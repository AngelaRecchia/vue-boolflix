<template>
  <div id="filterGenres">
    <div id="buttonG">
      <i class="fas fa-filter"></i> Genre:
      <span v-for="(picked, index) in pickedG" :key="index" class="nameG"
        >{{ picked.name }}
      </span>
    </div>

    <div id="showG">
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
      console.log(val.id);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
#filterGenres {
  margin: 20px 0;
}
#buttonG {
  background-color: black;
  border-radius: 5px;
  padding: 10px 15px;
  display: inline-block;
}
#listG {
  width: 40vw;
  height: 200px;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  font-size: 13px;
  padding: 15px;
  background-color: black;
  margin-top: 10px;
  border-radius: 5px;
}
</style>
