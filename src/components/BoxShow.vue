<template>
  <div class="box" v-if="show.vote_count > 20">
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
      <div class="vote">
        <i class="fas fa-star"></i> {{ show.vote_average }}
      </div>
      <div class="lang">
        <img :src="this.linkCountry" :alt="this.country" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "BoxShow",
  props: ["show"],
  data() {
    return {
      country: this.show.origin_Country[0],
      linkCountry:
        "https://www.countryflags.io/" + this.country + '/flat/64.png"',
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
    margin-top: -9px;
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
