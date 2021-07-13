<template>
  <div class="container">
    <div id="movies">
      <div class="row" v-if="movies.length > 0">
        <h4>Movies</h4>
        <BoxMovie
          v-for="(movie, index) in movies"
          :key="index"
          :movie="movie"
          class="col-4 col-md-3 col-lg-2"
        />
      </div>

      <div v-else>No results</div>
    </div>

    <div id="tvShows">
      <div class="row" v-if="tvShows.length > 0">
        <h4>TV Shows</h4>
        <BoxShow
          v-for="(show, index) in tvShows"
          :key="index"
          :show="show"
          class="col-4 col-md-3 col-lg-2"
        />
      </div>

      <div v-else>No results</div>
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
