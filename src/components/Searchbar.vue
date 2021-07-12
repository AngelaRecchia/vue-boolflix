<template>
  <div id="search">
    <input
      type="text"
      v-model="toSearch"
      @keyup.enter="$emit('search', toSearch)"
    />
    <div class="button ms-3" @click="$emit('search', toSearch)">Search</div>
  </div>
</template>

<script>
export default {
  name: "Searchbar",
  data() {
    return {
      toSearch: "",
    };
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";

input {
  width: 30vw;
  min-width: 200px;
  border-radius: 30px;
  height: 35px;
  padding: 0 20px;
  border: 2px solid black;
  color: $color2;
  background-color: $color3;

  &:focus {
    outline: none;
  }
}
.button {
  display: inline-block;
  padding: 8px 20px;
  border-radius: 20px;
  background-color: $color3;
  color: black;
  cursor: pointer;
  text-transform: uppercase;
  font-size: 13px;
}
</style>
