<template>
    <div class="wrapper" @keyup.enter="add"> 

      <section class="holecircles-input">
        <input v-model="input" id="input" type="text" maxlength="2">
        <div class="manage">
          <button id="btn-add" @click="add">+</button>
          <button id="btn-remove" v-on:click="remove">-</button>
        </div>
        <p>{{ errorMessage }}</p>
      </section>

      <section class="holecircles-output">
        <button id="holecircle" @click="input = hole" v-for="hole in holeCircles" :key="hole">{{hole}}</button>
      </section>
    </div>
</template>

<script>
export default {
  name: "Holecircles",
  data() {
    return {
      holeCircles: [],
      input: null,
      errorMessage: "error message"
    };
  },
  mounted() {
    //This block countinously refreshing the holeCircles array
    setInterval(() => {
      this.holeCircles = JSON.parse(localStorage.getItem("holeCircles"));
    }, 500);
  },
  methods: {
    //Add new holecircle to the array
    add() {
      if (this.isIncluded(this.input)) {
        console.log("Holecircle already included");
      } else if (!this.isValidInput(this.input)) {
        console.log("Invalid input");
      } else {
        this.holeCircles.push(this.input);
        this.holeCircles.sort();
        localStorage.setItem("holeCircles", JSON.stringify(this.holeCircles));
      }
    },
    //Remove a selected holecircle from the array
    remove() {
      if (!this.isIncluded(this.input)) {
        console.log("Holcircle is not on the list");
      } else if (!this.isValidInput(this.input)) {
        console.log("Invalid input");
      } else {
        this.holeCircles.splice(this.holeCircles.indexOf(this.input), 1);
        localStorage.setItem("holeCircles", JSON.stringify(this.holeCircles));
      }
    },
    //Check the input is valid
    isValidInput(input) {
      if (input == null || isNaN(input) || input.toString().length != 2) {
        return false;
      } else {
        return true;
      }
    },
    //Check a holcircle is on (or not on) the list
    isIncluded(input) {
      return this.holeCircles.includes(input);
    }
  }
};
</script>

<style scoped lang="scss">

  .wrapper {
    max-width: 960px;
    margin: 0 auto;
    section.holecircles-input {
      position: sticky;
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      margin: 10px auto;
      width: 205px;
      align-items: center;
      position: relative;
      left: 25px;
      #input {
        width: 100px;
        height: 100px;
        font-size: 60px;
      }
      .manage {
        display: grid;
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr;
        #btn-add, #btn-remove {
          width: 49px;
          height: 49px;
          margin: 2px;
          border: none;
          border-radius: 10%;
          background: grey;
          color: white;
          &:hover {
            background-color: black;
            color: lightgray;
          }
        }
      }
    }
    section.holecircles-output {
      #holecircle {
        width: 80px;
        height: 80px;
      }
    }
  }
</style>