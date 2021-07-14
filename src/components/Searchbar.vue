<template>
  <div id="search">
    <input
      type="text"
      v-model="toSearch"
      placeholder="Search movies or TV Shows"
      @keyup="$emit('search', toSearch)"
    />
    <i class="fas fa-search"></i>
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
#search {
  position: relative;
}
input {
  width: 20vw;
  min-width: 265px;
  border-radius: 30px;
  height: 40px;
  padding: 0 20px;
  border: 1px solid black;
  color: $color2;
  background-color: lighten($color2, $amount: 20%);
  transition: background-color 0.3s;
  transition: width 0.3s;

  &:focus {
    outline: none;
    width: 35vw;
  }
  &:hover {
    background-color: lighten($color2, $amount: 60%);
  }
}
i {
  color: $color2;
  cursor: pointer;
  font-size: 20px;
  position: absolute;
  right: 15px;
  top: 50%;
  transform: translateY(-50%);
}
</style>
