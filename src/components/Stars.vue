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
      this.piene = Math.floor(this.vote);
      this.half = this.vote - this.piene;
      this.vuote = 5 - this.piene;
      if (this.half > 0.2 && this.half < 0.8) {
        this.half = 1;
        this.vuote--;
      } else if (this.half <= 0.2) {
        this.half = 0;
      } else {
        this.piene++;
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
