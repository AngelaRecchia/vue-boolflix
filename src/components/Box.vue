<template>
  <div class="box">
    <img
      :src="'https://image.tmdb.org/t/p/w500' + show.poster_path"
      :alt="show.title"
    />
    {{ show.title }}
  </div>
</template>

<script>
export default {
  name: "Box",
  props: ["show"],
};
</script>

<style lang="scss" scoped>
.box {
  img {
    width: 100%;
  }
}
</style>
