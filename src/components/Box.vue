<template>
  <div class="box" v-if="show.vote_count > 20">
    <img
      :src="'https://image.tmdb.org/t/p/w500' + show.poster_path"
      :alt="show.title"
    />

    <div class="title">{{ show.title }}</div>
    <div class="orig-title">{{ show.original_title }}</div>
    <div class="vote">Rating: {{ show.vote_average }}</div>
    <div class="lang">{{ show.original_language }}</div>
  </div>
</template>

<script>
export default {
  name: "Box",
  props: ["show"],
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
.box {
  padding: 20px;
  background-color: rgba($color3, $alpha: 0.4);
  margin: 10px;
  color: black;
  img {
    width: 100%;
  }
  .title {
    font-weight: bold;
  }
  .orig-title {
    font-style: italic;
    font-size: 14px;
  }
  .lang {
    text-transform: uppercase;
  }
  .vote {
    font-size: 12px;
  }
  &:hover img {
    filter: brightness(50%);
  }
}
</style>
