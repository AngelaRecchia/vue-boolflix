<template>
  <div id="app">
    <Header @search="getSearch" />
    <Content
      :movies="searchMovies"
      :tvShows="searchShows"
      @searchGenre="searchGenre"
    />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header.vue";
import Content from "./components/Content.vue";

export default {
  name: "App",
  components: {
    Header,
    Content,
  },
  data() {
    return {
      titleToSearch: "",
      searchMovies: [],
      searchShows: [],
      loading: true,
      filt: [],
    };
  },
  mounted() {
    this.defaultMovies();
    this.defaultShows();
  },
  methods: {
    defaultMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1"
        )
        .then((result) => (this.searchMovies = result.data.results));
    },
    defaultShows() {
      axios
        .get(
          "https://api.themoviedb.org/3/tv/top_rated?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1"
        )
        .then((result) => (this.searchShows = result.data.results));
    },
    getSearch(title) {
      this.titleToSearch = title;
      if (title == "") this.defaultMovies();
      if (title == "") this.defaultShows();
      else {
        axios
          .get(
            "https://api.themoviedb.org/3/search/movie?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d",
            {
              params: {
                query: this.titleToSearch,
              },
            }
          )
          .then(
            (result) =>
              (this.searchMovies = result.data.results.filter(
                (elem) => elem.vote_count > 500
              ))
          );

        axios
          .get(
            "https://api.themoviedb.org/3/search/tv?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1",
            {
              params: {
                query: this.titleToSearch,
              },
            }
          )
          .then(
            (result) =>
              (this.searchShows = result.data.results.filter(
                (elem) => elem.vote_count > 500
              ))
          );

        this.loading = false;
      }
    },
    searchGenre(genre) {
      axios
        .get(
          "https://api.themoviedb.org/3/discover/movie?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&sort_by=popularity.desc&page=1",
          {
            params: {
              with_genres: genre,
            },
          }
        )
        .then((result) => (this.searchMovies = result.data.results));

      axios
        .get(
          "https://api.themoviedb.org/3/discover/tv?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&sort_by=popularity.desc&page=1",
          {
            params: {
              with_genres: genre,
            },
          }
        )
        .then((result) => (this.searchShows = result.data.results));
    },
  },
};
</script>

<style lang="scss">
@import "@/style/commons.scss";
#app {
  min-height: 100vh;
  background-color: $color2;
}
</style>
