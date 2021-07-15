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
      storedMovies: [],
      storedShows: [],
    };
  },
  mounted() {
    this.default();
  },
  methods: {
    default() {
      const topMovies =
        "https://api.themoviedb.org/3/movie/top_rated?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1";
      const topTV =
        "https://api.themoviedb.org/3/tv/top_rated?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1";
      axios.all([axios.get(topMovies), axios.get(topTV)]).then(
        axios.spread((resMovies, resTV) => {
          this.searchMovies = resMovies.data.results;
          this.searchShows = resTV.data.results;
        })
      );
    },

    getSearch(title) {
      this.titleToSearch = title;
      const apiSearchMovies =
        "https://api.themoviedb.org/3/search/movie?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d";
      const apiSearchTV =
        "https://api.themoviedb.org/3/search/tv?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d";
      const paramQuery = {
        params: {
          query: this.titleToSearch,
        },
      };

      if (this.titleToSearch == "") {
        this.default();
      } else {
        axios
          .all([
            axios.get(apiSearchMovies, paramQuery),
            axios.get(apiSearchTV, paramQuery),
          ])
          .then(
            axios.spread((resMovies, resTV) => {
              this.searchMovies = resMovies.data.results.filter(
                (elem) => elem.vote_count > 200
              );
              this.searchShows = resTV.data.results.filter(
                (elem) => elem.vote_count > 200
              );
            })
          );
      }
    },

    searchGenre(genre) {
      const genreMovies =
        "https://api.themoviedb.org/3/discover/movie?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&sort_by=popularity.desc&page=1";
      const genreTV =
        "https://api.themoviedb.org/3/discover/tv?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&sort_by=popularity.desc&page=1";
      const paramGenre = {
        params: {
          with_genres: genre,
        },
      };

      axios
        .all([
          axios.get(genreMovies, paramGenre),
          axios.get(genreTV, paramGenre),
        ])
        .then(
          axios.spread((resMovies, resTV) => {
            this.searchMovies = resMovies.data.results;
            this.searchShows = resTV.data.results;
          })
        );
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
