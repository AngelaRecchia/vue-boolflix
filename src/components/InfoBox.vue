<template>
  <b-tooltip :target="this.$parent" triggers="hover" placement="right">
    <div class="infos">
      <div class="title">{{ title }}</div>

      <Stars :rating="vote" class="stars text-center" />

      <div class="datas d-flex justify-content-between">
        <span>{{ duration }}</span>

        <span>{{ year.substring(0, 4) }}</span>

        <div class="lang">
          <img :src="linkCountry" :alt="country" />
        </div>
      </div>

      <div class="overview">{{ overview.substring(0, 180) }}...</div>

      <div class="genres">
        <span>Genres: </span>
        <span v-for="(genre, index) in genres" :key="index">
          <span class="genre" @click="$parent.$emit('searchGenre', genre.id)">{{
            genre.name
          }}</span>
          <span v-if="index < genres.length - 1">, </span>
        </span>
      </div>

      <div class="cast">
        <span>Cast: </span>
        <span v-for="(actor, index) in cast" :key="index">
          <span class="actor">{{ actor.name }}</span>
          <span v-if="index < cast.length - 1">, </span>
        </span>
      </div>
    </div>
  </b-tooltip>
</template>

<script>
import axios from "axios";
import Stars from "./Stars.vue";
export default {
  name: "InfoBox",
  props: ["type", "id"],
  components: {
    Stars,
  },
  data() {
    return {
      title: "",
      vote: "",
      year: "",
      duration: "",
      overview: "",
      genres: "",
      cast: "",
      country: "",
      linkCountry: "",
    };
  },
  mounted() {
    this.$nextTick(function () {
      if (this.type == "movie") {
        axios
          .get(
            "https://api.themoviedb.org/3/movie/" +
              this.id +
              "?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d"
          )
          .then((result) => {
            this.vote = result.data.vote_average;
            this.overview = result.data.overview;
            this.title = result.data.title;
            this.year = result.data.release_date;
            this.duration = result.data.runtime + "min";
            this.genres = result.data.genres;

            if (result.data.production_countries.length != 0) {
              this.country = result.data.production_countries[0].iso_3166_1;
            } else {
              this.country = result.data.original_language;
            }

            if (this.country.toLowerCase() == "en") this.country = "GB";

            this.linkCountry =
              "https://www.countryflags.io/" + this.country + "/flat/64.png";
          });

        axios
          .get(
            "https://api.themoviedb.org/3/movie/" +
              this.id +
              "/credits?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d"
          )
          .then((result) => (this.cast = result.data.cast.slice(0, 5)));
      } else {
        axios
          .get(
            "https://api.themoviedb.org/3/tv/" +
              this.id +
              "?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d"
          )
          .then((result) => {
            this.vote = result.data.vote_average;
            this.overview = result.data.overview;
            this.title = result.data.name;
            this.year = result.data.first_air_date;
            this.duration = result.data.episode_run_time + "min";
            this.genres = result.data.genres;
            this.country = result.data.origin_country[0];
            this.linkCountry =
              "https://www.countryflags.io/" + this.country + "/flat/64.png";
          });

        axios
          .get(
            "https://api.themoviedb.org/3/tv/" +
              this.id +
              "/credits?api_key=1dafa5cfbeee5c77b53b196c6bc8c45d"
          )
          .then((result) => (this.cast = result.data.cast.slice(0, 5)));
      }
    });
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
.infos {
  padding: 10px;
  text-align: left;
}
.title {
  font-size: 15px;
  font-weight: 700;
  text-align: center;
}
.datas,
.overview,
.genres,
.cast,
.stars {
  margin: 10px 0;
}
.overview {
  font-size: 12px;
}
.genres,
.cast {
  font-size: 13px;
}
.genre,
.actor {
  cursor: pointer;
  color: $color3;
}
.lang img {
  width: 20px;
  margin-top: -3px;
}
</style>
