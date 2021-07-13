<template>
  <div class="box">
    <div class="imgBox">
      <img
        class="poster"
        :src="'https://image.tmdb.org/t/p/w500' + show.poster_path"
        :alt="show.name"
      />

      <img
        class="play"
        src="https://img.icons8.com/ios-filled/50/000000/play-button-circled--v1.png"
      />
    </div>

    <div class="title">{{ show.name }}</div>
    <div class="orig-title">{{ show.original_name }}</div>
    <div class="miscInfos d-flex justify-content-between">
      <Stars :rating="show.vote_average" />

      <div class="lang">
        <img :src="linkCountry" :alt="country" />
      </div>
    </div>
  </div>
</template>

<script>
import Stars from "./Stars.vue";
export default {
  name: "BoxShow",
  props: ["show"],
  components: {
    Stars,
  },
  data() {
    return {
      country: this.show.origin_country[0],
      linkCountry:
        "https://www.countryflags.io/" +
        this.show.origin_country[0] +
        "/flat/64.png",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
.box {
  padding: 20px;
  color: $color3;
  line-height: 25px;
  .poster {
    width: 100%;
    transition: filter 0.5s;
    margin-bottom: 10px;
    border-radius: 10px;
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
