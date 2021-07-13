<template>
  <div class="box">
    <div class="imgBox">
      <img
        class="poster"
        :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
        :alt="movie.title"
      />

      <img
        class="play"
        src="https://img.icons8.com/ios-filled/50/000000/play-button-circled--v1.png"
      />
    </div>

    <div class="title">{{ movie.title }}</div>
    <div class="orig-title">{{ movie.original_title }}</div>
    <div class="miscInfos d-flex justify-content-between">
      <Stars :rating="movie.vote_average" />

      <div class="lang">
        <img :src="getURLCountry()" :alt="country" />
      </div>
    </div>

    <InfoBox type="movie" :id="movie.id" />
  </div>
</template>

<script>
import axios from "axios";
import Stars from "./Stars.vue";
import InfoBox from "./InfoBox.vue";
export default {
  name: "BoxMovie",
  props: ["movie"],
  components: {
    Stars,
    InfoBox,
  },
  data() {
    return {
      country: "",
    };
  },
  methods: {
    getURLCountry() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/" +
            this.movie.id +
            "?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d"
        )
        .then((result) => {
          if (result.data.production_countries.length != 0) {
            this.country = result.data.production_countries[0].iso_3166_1;
          } else {
            this.country = result.data.original_language;
          }

          if (this.country.toLowerCase() == "en") this.country = "GB";
        });
      return "https://www.countryflags.io/" + this.country + "/flat/64.png";
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
.box {
  padding: 20px;
  color: white;
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
