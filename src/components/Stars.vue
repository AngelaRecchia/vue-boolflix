<template>
  <div>
    <i
      v-for="(elem, index) in piene"
      :key="'piena' + index"
      class="fas fa-star"
    ></i>

    <i
      v-for="(elem, index) in half"
      :key="'half' + index"
      class="fas fa-star-half-alt"
    ></i>

    <i
      v-for="(elem, index) in vuote"
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
      piene: "",
      half: "",
      vuote: "",
      vote: this.rating / 2,
    };
  },
  mounted() {
    this.$nextTick(function () {
      let tempStar;
      this.piene = Math.floor(this.vote);
      tempStar = 5 - this.vote;
      this.vuote = Math.floor(tempStar);
      this.half = tempStar - this.vuote;
      if (this.half > 0.3 && this.half < 0.7) this.half = 1;
      else if (this.half <= 0.3) {
        this.half = 0;
      } else {
        this.vuote++;
        this.half = 0;
      }
    });
  },
};
</script>

<style lang="scss" scoped>
i {
  font-size: 12px;
  color: rgb(230, 189, 8);
}
</style>
