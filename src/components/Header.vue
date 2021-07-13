<template>
  <header>
    <div class="container d-flex align-items-center justify-content-between">
      <span id="logo">Boolflix</span>
      <Searchbar @search="search" />
    </div>
  </header>
</template>

<script>
import Searchbar from "./Searchbar.vue";
export default {
  name: "Header",
  components: {
    Searchbar,
  },
  methods: {
    search(text) {
      this.$emit("search", text);
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
header {
  background-color: black;
  .container {
    height: 100px;

    #logo {
      text-transform: uppercase;
      font-size: 35px;
      color: rgb(206, 7, 7);
    }
  }
}
</style>
