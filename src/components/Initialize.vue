<template>
  <div></div>
</template>

<script>
export default {
  name: "Initialize",
  props: ["holeCirclesArry"],
  data() {
    return {
      firstTimeRunning: true
    };
  },

  methods: {},

  created() {
    if (
      localStorage.getItem("holeCircles") == null ||
      localStorage.getItem("language") == null ||
      localStorage.getItem("theme") == null
    ) {
      this.firstTimeRunning = true;
    } else {
      this.firstTimeRunning = false;
    }

    if (this.firstTimeRunning == true) {
      setTimeout(() => {
        localStorage.setItem("holeCircles", this.holeCirclesArry);
        localStorage.setItem("language", "en");
        localStorage.setItem("theme", "light");
      }, 0);
    }
  }
};
</script>

<style lang="scss">
</style>