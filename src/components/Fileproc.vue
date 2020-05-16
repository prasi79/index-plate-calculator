<template>
  <div>
  </div>
</template>

<script>
import jsonHoleCircles from "../assets/json/holeCircles.json";

export default {
  name: "Fileproc",
  props: ["holeCirclesArry"],
  data() {
    return {};
  },
  created() {
    this.$emit("initHoleCirclesArry", JSON.stringify(jsonHoleCircles));
  }
};
</script>

<style lang="scss">
</style>