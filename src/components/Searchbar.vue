<template>
  <div id="search" class="text-center">
    <input type="text" v-model="toSearch" />
    <div class="btn btn-dark" @click="$emit('search', toSearch)">Search</div>
  </div>
</template>

<script>
export default {
  name: "Searchbar",
  data() {
    return {
      toSearch: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
</style>
