<template>
  <div class="container">
    <div id="movies">
      <h4>Movies</h4>
      <div class="row" v-if="movies.length > 0">
        <BoxMovie
          v-for="movie in movies"
          :key="movie.id"
          :movie="movie"
          class="col-4 col-md-3 col-lg-2"
        />
      </div>

      <div v-else class="text-center">No results</div>
    </div>

    <div id="tvShows">
      <h4>TV Shows</h4>
      <div class="row" v-if="tvShows.length > 0">
        <BoxShow
          v-for="show in tvShows"
          :key="show.id"
          :show="show"
          class="col-4 col-md-3 col-lg-2"
        />
      </div>

      <div v-else class="text-center">No results</div>
    </div>
  </div>
</template>

<script>
import BoxMovie from "./BoxMovie.vue";
import BoxShow from "./BoxShow.vue";
export default {
  name: "Content",
  props: ["movies", "tvShows"],
  components: {
    BoxMovie,
    BoxShow,
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
div {
  color: $color3;
}
</style>
