<template>
  <div class="wrapper">
    <section class="input">
      <div id="divsrequied-text">Division <br> requied</div>
      <div id="divsrequied-input"><input v-on:keyup="calculation()" v-model="input.division" type="number"></div>
      <div id="gearratio-text">Gear ratio</div>
      <div id="gearratio-input"><input v-on:keyup="calculation()" v-model="input.gearRatio" type="number"></div>
    </section>
    
    <section class="output">
      <section class="fullrevs">
        <div id="fullrevs-text">Full revs.</div>
        <div id="fullrevs-output">{{ this.output.wholeNum }}</div>
        <div id="and-text">and</div>
      </section>

      <section class="remainder">
        <div id="remainder-output">{{ this.output.remain }}</div>
      </section>
    </section>
  </div>
</template>

<script>
export default {
  name: "Calculator",
  data() {
    return {
      input: {
        division: "",
        gearRatio: ""
      },
      output: {
        wholeNum: "-",
        remain: ""
      }
    };
  },
  methods: {
    calculation: function() {
      // Validate the inputs
      if (
        Number.isNaN(parseFloat(this.input.division)) ||
        Number.isNaN(parseFloat(this.input.gearRatio))
      ) {
        this.output.wholeNum = "-";
        this.output.remain = "";
      } else {
        // Calculate the remainders
        let founded = new Set();
        let numerator = this.input.gearRatio % this.input.division;

        for (let iM = 1; iM <= 30; iM++) {
          let multNumerator = numerator * iM;
          let multDenominator = this.input.division * iM;

          for (let iD = 1; iD <= 30; iD++) {
            let divNumerator = multNumerator / iD;
            let divDenominator = multDenominator / iD;

            for (let hole of JSON.parse(localStorage.getItem("holeCircles"))) {
              if (
                divDenominator == hole &&
                divNumerator % 1 == 0 &&
                divNumerator != 0
              ) {
                var result =
                  "on the " +
                  divDenominator +
                  " holecircle turn " +
                  divNumerator +
                  " holes. ";
              }
              founded.add(result);
            }
          }
        }
        founded = Array.from(founded);
        founded.sort();
        founded = founded.toString();
        founded = founded.replace(/,/g, "");

        if (founded == "") {
          founded = "no further turns requied.";
        }

        // Calculate the whole number
        this.output.wholeNum = Math.floor(
          this.input.gearRatio / this.input.division
        );
        this.output.remain = founded;
      }
    }
  }
};
</script>

<style scoped lang="scss">

$breakpoint-tablet: 650px;
$breakpoint-phone: 500px;
$breakpoint-smallscreen: 420px;

.wrapper {
  max-width: 960px;
  margin: 0 auto;

  section.input{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    align-items: center;
    margin: 10px auto;
    max-width: 50%;
    min-width: 380px;
  }

  section.output {
    display: grid;
    grid-template-columns: 1fr auto;
    margin: 20px auto;
    max-width: 70%;
    min-width: 620px;
    
    section.fullrevs{
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      align-items: center;
      height: 80px;
      #fullrevs-output {
        color: salmon;
        font-size: 80px;
      }
    }
    section.remainder {
      display: grid;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr;
      margin: 0 0 0 15px;
      #remainder-output {
        width: 403px;
        color: salmon;
        font-size: 25px;
      }
    }
  }
}

@media (max-width: $breakpoint-tablet) {
  .wrapper {
    section.input {
      margin: 10px auto;
      max-width: 70%;
    }
    section.output {
      grid-template-columns: 1fr;
      grid-template-rows: 100px 1fr;
      min-width: 450px;
      section.fullrevs {
        margin: 0 auto;
        max-width: 60%;
        #fullrevs-text {
          font-size: 40px;
        }
        #fullrevs-output {
          font-size: 80px;
        }
        #and-text{
          font-size: 50px;
        }
      }
      section.remainder {
        margin: 0 auto;
      }
    }
  }
}

@media (max-width: $breakpoint-phone) {
  .wrapper {
    section.input {
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      margin: 10px auto;
      min-width: 250px;
      max-width: 56%;
    }
    section.output {
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr;
      min-width: 400px;
      section.fullrevs {
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr 1fr;
        #fullrevs-output {
          margin: -10px 0 -15px 0;
        }
      }
    }
    section.remainder {
      position: relative;
      bottom: 30px;
    }
  }
}

@media (max-width: $breakpoint-smallscreen) {
  .wrapper {
    section.output {
      grid-template-rows: 170px 1fr;
      min-width: 300px;
      section.remainder {
        bottom: 0px;
        #remainder-output {
          font-size: 18px;
          max-width: 300px;
        }
      }
      
    }
  }
}
</style>