<template>
  <div class="box" v-if="show.vote_count > 20">
    <div class="imgBox">
      <img
        class="poster"
        :src="'https://image.tmdb.org/t/p/w500' + show.poster_path"
        :alt="show.title"
      />

      <img
        class="play"
        src="https://img.icons8.com/ios-filled/50/000000/play-button-circled--v1.png"
      />
    </div>

    <div class="title">{{ show.title }}</div>
    <div class="orig-title">{{ show.original_title }}</div>
    <div class="vote">Rating: {{ show.vote_average }}</div>
    <div class="lang">
      <img
        v-if="show.original_language == 'en'"
        src="https://www.countryflags.io/us/flat/64.png"
        alt="en"
      />
      <img
        v-else
        :src="
          'https://www.countryflags.io/' +
          show.original_language +
          '/flat/64.png'
        "
        :alt="show.original_language"
      />
    </div>
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
  .poster {
    width: 100%;
    transition: filter 0.5s;
  }
  .title {
    font-weight: bold;
  }
  .orig-title {
    font-style: italic;
    font-size: 14px;
  }
  .lang img {
    width: 20px;
  }
  .vote {
    font-size: 12px;
  }
  .imgBox {
    position: relative;
  }
  .play {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    border-radius: 50%;
    opacity: 0;
    transition: opacity 0.5s;
    cursor: pointer;
  }
  &:hover .poster {
    filter: brightness(50%);
  }
  &:hover .play {
    opacity: 1;
  }
}
</style>
