<template>
  <b-tooltip :target="this.$parent" triggers="hover" placement="right">
    <div class="infos">
      <span class="title">{{ title }}</span>
      <div class="datas d-flex justify-content-between">
        <span><i class="fas fa-star"></i> {{ vote }}</span>
        <span>{{ year.substring(0, 4) }}</span>
      </div>
      <div class="overview">
        <strong>Overview:</strong> {{ overview.substring(0, 200) }}...
      </div>
    </div>
  </b-tooltip>
</template>

<script>
export default {
  name: "InfoBox",
  props: ["title", "year", "vote", "overview"],
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
