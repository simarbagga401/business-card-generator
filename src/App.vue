<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard ref="businessCard">
    <h2 id="card-heading" @click="activeEl = 'card-heading'">business card</h2>

    <DDR
      v-model="pProperties"
      :parent="true"
      :minWidth="1"
      :active="transformActive"
      :y="130"
    >
      <p id="card-description" @click="activeEl = 'card-description'">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eligendi,
        quas?
      </p>
    </DDR>
  </BusinessCard>

  <!-- Modify Selected Element -->
  <h3>Modify Selected Element :</h3>
  <p><strong>Selected Element:</strong> {{ activeEl }}</p>
  <div class="color-picker" />

  <!-- Change Card Color -->
  <h3>Change Border Radius:</h3>
  <input
    type="range"
    v-model="sliderValue"
    min="0"
    max="50"
    @input="this.$refs.businessCard.changeBorderRadius(sliderValue)"
  />

  <!-- Download BusinessCard -->
  <h3>Download Card :</h3>
  <button class="btn" @click="saveCardAsImage('png')">
    Download Card As png
  </button>
  <button class="btn" @click="saveCardAsImage('jpeg')">
    Download Card As jpeg
  </button>
</template>

<script>
import BusinessCard from "./components/BusinessCard.vue";
//importing library to make elements movable
import DDR from "yoyoo-ddr-vue3";
import "yoyoo-ddr-vue3/dist/yoyoo-ddr-vue3.css";
//importing pickr
import "@simonwep/pickr/dist/themes/monolith.min.css";
import Pickr from "@simonwep/pickr";
export default {
  components: {
    BusinessCard,
    DDR,
  },
  data() {
    return {
      sliderValue: 0,
      pProperties: { x: 100, y: 100, width: 200, height: 100, rotation: 0 },
      transformActive: true,
      activeEl: "",
    };
  },
  methods: {
    saveCardAsImage(imageFormat) {
      this.transformActive = false;
      setTimeout(() => {
        console.log("waiting");
        this.$refs.businessCard.printCard(imageFormat);
        this.transformActive = true;
      }, 1000);
    },
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
      pickr.on("change", (instance) => {
        document.getElementById(this.activeEl).style.color = instance.toHEXA();
      });
    },
  },
  mounted() {
    this.initPickr();
    // APPLY IMAGE TO CARD BACKGROUND
    this.$refs.businessCard.changeBackground(
      "image",
      "../src/assets/flower-background.jpg"
    );
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
