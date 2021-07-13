<template>
  <div>
    <i
      v-for="(elem, index) in vote"
      :key="'piena' + index"
      class="fas fa-star"
    ></i>
    <i
      v-for="(elem, index) in 5 - vote"
      :key="'vuota' + index"
      class="far fa-star"
    ></i>
  </div>
</template>

<script>
export default {
  name: "Stars",
  props: ["rating"],
  data() {
    return {
      vote: Math.round(this.rating / 2),
    };
  },
};
</script>

<style lang="scss" scoped>
i {
  font-size: 12px;
  color: rgb(230, 189, 8);
}
</style>
