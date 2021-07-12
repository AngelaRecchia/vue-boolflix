<template>
  <div id="app">
    <Header @search="getSearch" />
    <Content :shows="searchResults" />
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
      searchResults: [],
      loading: true,
    };
  },
  mounted() {
    axios
      .get(
        "https://api.themoviedb.org/3/movie/top_rated?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d&page=1"
      )
      .then((result) => (this.searchResults = result.data.results));
  },
  methods: {
    getSearch(title) {
      this.titleToSearch = title;
      axios
        .get(
          "https://api.themoviedb.org/3/search/movie?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d",
          {
            params: {
              query: this.titleToSearch,
            },
          }
        )
        .then((result) => (this.searchResults = result.data.results));

      this.loading = false;
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
