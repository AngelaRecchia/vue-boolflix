<template>
  <div id="filterGenres">
    <div id="buttonG">
      <i class="fas fa-filter"></i> Genre:
      <span v-for="(picked, index) in pickedG" :key="index" class="nameG"
        >{{ picked.name }}
      </span>
    </div>

    <b-tooltip target="buttonG" triggers="click" placement="bottomleft">
      <b-form-group v-model="pickedG">
        <b-form-checkbox-group id="pickG" v-model="pickedG">
          <b-form-checkbox
            v-for="(genre, index) in options"
            :key="index"
            :value="genre"
            >{{ genre.name }}</b-form-checkbox
          >
        </b-form-checkbox-group>
      </b-form-group>
    </b-tooltip>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "PickGenres",
  data() {
    return {
      pickedG: ["All"],
      options: [],
    };
  },
  mounted() {
    this.$nextTick(function () {
      const all = { id: 0, name: "All" };
      const listGMovies =
        "https://api.themoviedb.org/3/genre/movie/list?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d";

      axios.get(listGMovies).then((res) => {
        this.options = [all, ...res.data.genres];
      });
    });
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
</style>
