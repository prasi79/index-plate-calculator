<template>
  <div class="wrapper">
    <section class="input-section">
      <div id="divs-requied-text">Division <br> requied</div>
      <div id="divs-requied-input"><input v-on:keyup="calculation()" v-model="input.division" type="number"></div>
      <div id="gear-ratio-text">Gear ratio</div>
      <div id="gear-ratio-input"><input v-on:keyup="calculation()" v-model="input.gearRatio" type="number"></div>
    </section>
    
    <section class="output-section">
      <section class="full-revs-section">
        <div id="full-revs-text">Full revs.</div>
        <div id="full-revs-output">{{ this.output.wholeNum }}</div>
        <div id="and-text">and</div>
      </section>

      <section class="remainder-section">
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

<style lang="scss">

$breakpoint-tablet: 550px;
$breakpoint-phone: 450px;
$breakpoint-smallscreen: 390px;

.wrapper {
  max-width: 500px;
  margin: 0 auto;

  .input-section{
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    align-items: center;
    text-align: center;
    margin: 10px 50px 0px 50px;
    position: relative;
    left: 0px;
  }

  .output-section {
    display: grid;
    grid-template-columns: 1fr 340px;
    text-align: center;
    margin-top: 10px;
    position: relative;
    left: 0px;
    .full-revs-section{
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      align-items: center;
      height: 58px;
      #full-revs-output {
        color: salmon;
        font-size: 50px;
      }
    }
    .remainder-section {
      display: grid;
      grid-template-columns: 1fr;
      grid-template-rows: 1fr;
      margin: 0 auto;
      #remainder-output {
        width: 340px;
        color: salmon;
      }
    }
  }
}

@media (max-width: $breakpoint-tablet) {
  .wrapper {
    .input-section {
      margin: 20px auto;
      max-width: 70%;
    }
    .output-section {
      grid-template-columns: 1fr;
      grid-template-rows: 92px 1fr;
      .full-revs-section {
        margin: 0px auto;
        max-width: 65%;
        #full-revs-text {
          font-size: 40px;
        }
        #full-revs-output {
          font-size: 80px;
        }
        #and-text{
          font-size: 50px;
        }
      }
    }
  }
}

@media (max-width: $breakpoint-phone) {
  .wrapper {
    .input-section {
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr 1fr;
      margin: 0px auto;
      max-width: 65%;
      width: 210px;
      div {
       margin: 5px 0;
      }
    }
    .output-section {
      grid-template-columns: 1fr;
      grid-template-rows: 1fr 1fr;
      .full-revs-section {
        grid-template-columns: 1fr;
        grid-template-rows: 1fr 1fr 1fr;

        #full-revs-output {
          margin: -10px 0 -25px 0;
        }
      }
    }
  }
}

@media (max-width: $breakpoint-smallscreen) {
  .wrapper {
    .output-section {
      grid-template-rows: 170px 1fr;
      .remainder-section {
        #remainder-output {
          font-size: 18px;
          width: 300px;
        }
      }
      
    }
  }
}
</style>