<template>
  <div class="container">
    <div id="movies" class="py-4">
      <h4>Movies</h4>
      <div class="row" v-if="movies.length > 0">
        <Box
          v-for="movie in movies"
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
export default {
  name: "Content",
  props: ["movies", "tvShows"],
  components: {
    Box,
  },
  methods: {
    searchGenre(genre) {
      this.$emit("searchGenre", genre);
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
