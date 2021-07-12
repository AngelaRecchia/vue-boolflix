<template>
  <div id="box">
    {{ show.title }}
  </div>
</template>

<script>
export default {
  name: "Box",
  props: ["show"],
};
</script>

<style lang="scss" scoped></style>
