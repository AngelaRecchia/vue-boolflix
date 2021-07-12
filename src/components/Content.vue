<template>
  <div class="container">
    <div v-if="shows.length > 0" class="row">
      <Box
        v-for="(show, index) in shows"
        :key="index"
        :show="show"
        class="col-4 col-md-3 col-lg-2"
      />
    </div>

    <div v-else>No results</div>
  </div>
</template>

<script>
import Box from "./Box.vue";
export default {
  name: "Content",
  props: ["shows"],
  components: {
    Box,
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
div {
  color: $color3;
}
</style>
