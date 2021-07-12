<template>
  <div class="container">
    <Box v-for="(show, index) in shows" :key="index" :show="show" />
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
