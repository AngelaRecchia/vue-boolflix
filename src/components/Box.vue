<template>
  <div id="box">
    <div class="imgBox">
      <img
        class="poster"
        :src="'https://image.tmdb.org/t/p/w500' + poster"
        :alt="title"
      />

      <img
        class="play"
        src="https://img.icons8.com/ios-filled/50/000000/play-button-circled--v1.png"
      />
    </div>

    <div class="title">{{ title }}</div>

    <div class="vote"><i class="fas fa-star"></i> {{ vote }}</div>

    <InfoBox :type="type" :id="id" />
  </div>
</template>

<script>
import InfoBox from "./InfoBox.vue";
export default {
  name: "Box",
  props: ["id", "title", "orig", "poster", "vote", "type"],
  components: {
    InfoBox,
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
#box {
  padding: 20px;
  color: lighten($color2, $amount: 70%);
  line-height: 25px;
  font-family: "Quicksand", sans-serif;
  .poster {
    width: 100%;
    transition: filter 0.5s;
    margin-bottom: 10px;
    border-radius: 10px;
  }
  .title {
    font-weight: bold;
  }
  .vote {
    font-size: 13px;
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
