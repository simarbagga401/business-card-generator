<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard ref="businessCard" />
  <!-- <MovableTest /> -->

  <!-- Change Card Color -->
  <p>Change Background of Card :</p>
  <div class="color-picker"></div>
  <button class="btn" @click="this.$refs.businessCard.changeBackground(pickedColor)">Apply</button>

  <!-- Download BusinessCard -->
  {{pickedColor}}
  <p>Download Card :</p>
  <button class="btn" @click="this.$refs.businessCard.saveCardAsImage('png')">
    Download Card As png
  </button>
  <button class="btn" @click="this.$refs.businessCard.saveCardAsImage('jpeg')">
    Download Card As jpeg
  </button>
</template>

<script>
import BusinessCard from "./components/BusinessCard.vue";
import MovableTest from "./components/MovableTest.vue";
//importing pickr
import "@simonwep/pickr/dist/themes/monolith.min.css";
import Pickr from "@simonwep/pickr";
export default {
  components: {
    BusinessCard,
    MovableTest
},
  data(){
    return{
      pickedColor:'',
    }
  },
  methods: {
    initPickr() {
      const pickr = Pickr.create({
        el: ".color-picker",
        theme: "monolith", // or 'monolith', or 'nano'

        swatches: [
          "rgba(244, 67, 54, 1)",
          "rgba(233, 30, 99, 0.95)",
          "rgba(156, 39, 176, 0.9)",
          "rgba(103, 58, 183, 0.85)",
          "rgba(63, 81, 181, 0.8)",
          "rgba(33, 150, 243, 0.75)",
          "rgba(3, 169, 244, 0.7)",
        ],

        components: {
          // Main components
          preview: true,
          opacity: true,
          hue: true,

          // Input / output Options
          interaction: {
            hex: true,
            input: true,
            clear: true,
            save: true,
          },
        },
      });
      pickr.on('change',instance => {
        this.pickedColor = instance.toHEXA();
      })
    },
  },
  mounted() {
    this.initPickr();
  },
};
</script>

<style>
#app {
  font-family: "poppins";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #2c2c2c;
  margin-top: 60px;
}

.btn {
  padding: 10px 15px;
  margin: 5px;
  background: rgb(205, 252, 255);
  border: 1px solid rgb(65, 217, 255);
  border-radius: 10px;
}
.btn.active {
  border: 1px solid rgb(109, 255, 109);
  background: rgb(212, 255, 212);
}
</style>
