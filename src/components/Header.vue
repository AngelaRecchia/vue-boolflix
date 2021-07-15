<template>
  <header>
    <div class="container d-flex align-items-center justify-content-between">
      <div class="d-flex align-items-center">
        <span id="logo" @click="refresh">Boolflix</span>
        <ul>
          <li @click="selectedM" :class="{ borderR: mActive }">Movies</li>
          <li @click="selectedTV" :class="{ borderR: tvActive }">TV Shows</li>
        </ul>
      </div>

      <Searchbar @search="search" />
    </div>
  </header>
</template>

<script>
import Searchbar from "./Searchbar.vue";
export default {
  name: "Header",
  data() {
    return {
      mActive: true,
      tvActive: false,
    };
  },
  components: {
    Searchbar,
  },
  methods: {
    search(text) {
      this.$emit("search", text);
    },
    refresh() {
      window.location.reload();
    },
    selectedM() {
      this.mActive = true;
      this.tvActive = false;
      this.$emit("showM");
    },
    selectedTV() {
      this.mActive = false;
      this.tvActive = true;
      this.$emit("showTV");
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/style/commons.scss";
header {
  background-color: black;
  .container {
    height: 100px;

    #logo {
      cursor: pointer;
      text-transform: uppercase;
      font-size: 35px;
      color: rgb(206, 7, 7);
    }
    ul {
      display: inline-block;
      margin-bottom: 0;
    }
    li {
      color: lighten($color2, $amount: 70%);
      display: inline;
      font-size: 16px;
      margin: 0 20px;
      cursor: pointer;
      padding: 0 10px;
      padding-bottom: 37px;
    }
    .borderR {
      border-bottom: 2px solid rgb(206, 7, 7);
    }
  }
}
</style>
