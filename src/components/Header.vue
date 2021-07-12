<template>
  <header class="d-flex align-items-center justify-content-center">
    <Searchbar @search="search" />
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
  height: 100px;
}
</style>
