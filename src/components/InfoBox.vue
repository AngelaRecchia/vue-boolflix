<template>
  <b-tooltip :target="this.$parent" triggers="hover" placement="right">
    <div class="infos">
      <span class="title">{{ title }}</span>
      <div class="datas d-flex justify-content-between">
        <span><i class="fas fa-star"></i> {{ vote }}</span>
        <span>{{ duration }}</span>
        <span>{{ year.substring(0, 4) }}</span>
      </div>
      <div class="overview">
        <strong>Overview:</strong> {{ overview.substring(0, 200) }}...
      </div>
    </div>
  </b-tooltip>
</template>

<script>
import axios from "axios";
export default {
  name: "InfoBox",
  props: ["type", "id"],
  data() {
    return {
      title: "",
      vote: "",
      year: "",
      duration: "",
      overview: "",
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
          });
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
          });
      }
    });
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
.infos {
  padding: 10px;
}
.title {
  font-size: 15px;
  font-weight: 700;
}
.datas {
  margin: 10px 0;
}
</style>
