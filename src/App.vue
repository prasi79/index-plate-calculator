<template>
  <div id="app">
    <fileprocess
      v-bind:holeCirclesArry="holeCirclesArry"
      v-on:initHoleCirclesArry="initHoleCirclesArry($event)"
    ></fileprocess>
    <initialize v-bind:holeCirclesArry="holeCirclesArry"></initialize>
    <app-header />
    <router-view />
  </div>
</template>

<script>
import Fileprocess from "./components/Fileproc.vue";
import Initialize from "./components/Initialize.vue";
import Header from "./components/layout/Header";

export default {
  name: "App",
  components: {
    fileprocess: Fileprocess,
    initialize: Initialize,
    "app-header": Header
  },
  data() {
    return {
      holeCirclesArry: []
    };
  },
  methods: {
    initHoleCirclesArry(holeCirclesArry) {
      this.holeCirclesArry = holeCirclesArry;
    }
  }
};
</script>

<style lang="scss">
*{
    color: rgb(125, 186, 133);
    font-family: Arial, Helvetica, sans-serif;
    font-weight: bold;
    font-size: 30px;
    list-style-type: none;
    &:hover {
      cursor: default;
    }
  }

  body {
    background: rgb(240, 240, 240);
    margin: 0 auto;
    text-align: center;
  }

  input {
    font-size: 30px;
    height: 55px;
    width: 50px;
    text-align: center;
    
    border: none;
    border-radius: 10%;
    background: grey;
    color: white;
    &:hover {
      background-color: black;
      color: lightgray;
    }
  }

  /*Turn off input spinners*/
  /* Chrome, Safari, Edge, Opera */
  input::-webkit-outer-spin-button,
  input::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }

  /* Firefox */
  input[type=number] {
    -moz-appearance: textfield;
  }
</style>
