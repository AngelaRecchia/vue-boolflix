<template>
  <div class="container">
    <div class="row">
      <Box
        v-for="(show, index) in shows"
        :key="index"
        :show="show"
        class="col-4 col-md-3 col-lg-2"
      />
    </div>
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

<style lang="scss" scoped></style>
