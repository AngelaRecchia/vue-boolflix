<template>
  <div id="filterGenres">
    <div id="buttonG" class="button" @click="showing = !showing">
      <i class="fas fa-filter"></i> Genre:
      <span v-for="(picked, index) in pickedG" :key="index" class="nameG"
        >{{ picked.name }}<span v-if="index < pickedG.length - 1">, </span>
      </span>
    </div>

    <div id="showG" v-if="showing">
      <b-form-group v-model="pickedG">
        <b-form-checkbox-group v-model="pickedG" id="listG">
          <b-form-checkbox
            class="elemCheck"
            v-for="(genre, index) in options"
            :key="index"
            :value="genre"
            @change="check(genre)"
            ><span class="ms-1">{{ genre.name }}</span>
          </b-form-checkbox>
        </b-form-checkbox-group>
      </b-form-group>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PickGenres",
  data() {
    return {
      all: { id: 0, name: "All" },
      pickedG: [],
      options: [],
      showing: false,
    };
  },
  mounted() {
    this.$nextTick(function () {
      this.pickedG.push(this.all);

      const listGMovies =
        "https://api.themoviedb.org/3/genre/movie/list?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d";

      axios.get(listGMovies).then((res) => {
        this.options = [this.all, ...res.data.genres];
      });
    });
  },
  updated() {
    if (this.pickedG.length == 0) this.pickedG.push(this.all);
    this.$emit("filterGenres", this.pickedG);
  },
  methods: {
    check(val) {
      if (val.id != 0 && this.pickedG.includes(this.all)) {
        this.pickedG.splice(
          this.pickedG.findIndex((elem) => elem == this.all),
          1
        );
      }
      if (val.id == 0) this.pickedG = [this.all];
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
#filterGenres {
  margin-top: 20px;
  font-size: 14px;
  position: relative;
}
.button {
  border-radius: 5px;

  display: inline-block;
  font-weight: 600;
  cursor: pointer;
}
#buttonG {
  background-color: black;
  padding: 10px 15px;
}
#filter {
  padding: 5px 10px;
  font-size: 12px;
  color: black;
  position: absolute;
  right: 30px;
  bottom: 20px;
  background-color: lighten($color2, $amount: 50%);
  &:hover {
    background-color: lighten($color2, $amount: 60%);
  }
}
#showG {
  position: absolute;
  top: 40px;
  width: 500px;
  z-index: 2;
  padding: 15px;
  background-color: rgba($color: #000000, $alpha: 0.85);
  margin-top: 10px;
  border-radius: 5px;
}
#listG {
  height: 180px;
  display: inline-flex;
  flex-direction: column;
  flex-wrap: wrap;
  font-size: 13px;
  & > * {
    padding: 5px 10px;
    border-radius: 5px;
    &:hover {
      background-color: rgba($color: #000000, $alpha: 0.9);
    }
  }
}
</style>
