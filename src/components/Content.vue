<template>
  <div class="container">
    <PickGenres @filterGenres="filterGenres" />

    <div id="movies" class="py-4">
      <h4>Movies</h4>
      <div class="row" v-if="movies.length > 0">
        <Box
          v-for="movie in movies"
          v-show="toFilter(movie)"
          :key="movie.id"
          :id="movie.id"
          :poster="movie.poster_path"
          :title="movie.title"
          :orig="movie.original_title"
          :vote="movie.vote_average"
          type="movie"
          class="col-4 col-md-3 col-lg-2"
          @searchGenre="searchGenre"
        />
      </div>

      <div v-else class="text-center">No results</div>
    </div>

    <div id="tvShows" class="py-4">
      <h4>TV Shows</h4>
      <div class="row" v-if="tvShows.length > 0">
        <Box
          v-for="show in tvShows"
          v-show="toFilter(show)"
          :key="show.id"
          :id="show.id"
          :poster="show.poster_path"
          :title="show.name"
          :orig="show.original_name"
          :vote="show.vote_average"
          :type="show"
          class="col-4 col-md-3 col-lg-2"
          @searchGenre="searchGenre"
        />
      </div>

      <div v-else class="text-center">No results</div>
    </div>
  </div>
</template>

<script>
import Box from "./Box.vue";
import PickGenres from "./Genres.vue";
export default {
  name: "Content",
  props: ["movies", "tvShows"],
  data() {
    return {
      gen: [0],
    };
  },
  components: {
    Box,
    PickGenres,
  },
  methods: {
    searchGenre(genre) {
      this.$emit("searchGenre", genre);
    },
    filterGenres(genres) {
      this.gen = genres.map((elem) => elem.id);
      console.log(this.gen);
    },
    toFilter(movie) {
      if (this.gen.includes(0)) return true;
      else if (this.gen.length != 0) {
        return this.gen.every((el) => movie.genre_ids.includes(el));
      } else return false;
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
div {
  color: $color3;
}
</style>
