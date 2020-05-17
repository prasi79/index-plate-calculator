<template>
    <div class="wrapper">
      <section class="holecircles-input">
        <input v-model="input" id="input" type="number">
        <div class="manage">
          <button id="btn-add" v-on:click="add">+</button>
          <button id="btn-remove" v-on:click="remove">-</button>
        </div>
      </section>

      <section class="holecircles-output">
        <button id="holecircles" v-on:click="input = hole" v-for="hole in holeCircles" :key="hole">{{hole}}</button>
      </section>
    </div>
</template>

<script>
export default {
  name: "Holecircles",
  data() {
    return {
      holeCircles: [],
      input: null
    };
  },
  mounted() {
    //This block countinously refreshing the holeCircles array
    setInterval(() => {
      this.holeCircles = JSON.parse(localStorage.getItem("holeCircles"));
    }, 500);

    //Need to be debug this block, the code can't find the "add()" function
    window.addEventListener("keypress", function(e) {
      if (e.key == "Enter") {
        this.add;
        console.log("yeet");
      }
    });
  },
  methods: {
    //Add new hole circle to the array
    //Need some input check
    add() {
      this.holeCircles.push(this.input);
      this.holeCircles.sort();
      localStorage.setItem("holeCircles", JSON.stringify(this.holeCircles));
    },
    //Remove a selecteh hole circle from the array
    //Need some input check
    remove() {
      this.holeCircles.splice(this.holeCircles.indexOf(this.input), 1);
      localStorage.setItem("holeCircles", JSON.stringify(this.holeCircles));
    }
  }
};
</script>

<style scoped lang="scss">

  .wrapper {
    max-width: 960px;
    margin: 0 auto;
    section.holecircles-input {
      display: grid;
      grid-template-columns: 1fr 1fr;
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
  }
</style>