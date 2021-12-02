<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard ref="businessCard">
    <DDR
      :value="h2Properties"
      :parent="true"
      :minWidth="1"
      :active="cardHeadingActive"
      :y="130"
    >
      <h2 id="cardHeading" @click="activeEl = 'cardHeading'">Google, Pvt</h2>
    </DDR>

    <DDR
      :value="pProperties"
      :parent="true"
      :minWidth="1"
      :active="cardDescriptionActive"
      :y="130"
    >
      <p id="cardDescription" @click="activeEl = 'cardDescription'">
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eligendi,
        quas?
      </p>
    </DDR>
  </BusinessCard>

  <!-- Download BusinessCard -->
  <h3>Download Card :</h3>
  <button class="btn" @click="saveCardAsImage('png')">
    Download Card As png
  </button>
  <button class="btn" @click="saveCardAsImage('jpeg')">
    Download Card As jpeg
  </button>

  <!-- Modify Selected Element -->
  <h3>Modify Selected Element :</h3>
  <p><strong>Selected Element:</strong> {{ activeEl }}</p>
  <div class="modify-properties-container">
    <p>Color:</p>
    <div class="color-picker" />
    <button @click="applyBorderColor()">apply color to card border</button>
    <br />
    <button @click="changeFontProperties('fontWeight', 'bold')">Bold</button>
    <button @click="changeFontProperties('fontStyle', 'italic')">Italic</button>
    <button @click="changeFontProperties('textDecoration', 'underline')">
      Underlilne
    </button>
    <br />
    <button @click="deleteActiveEl()">Delete</button>
    <br />
    <p>Font Size: (number)</p>
    <input
      @change="changeFontProperties('fontSize', fontSize)"
      type="number"
      placeholder="font-size"
      v-model="fontSize"
      min="4"
    />
    <br />
    <select
      v-model="fontFamily"
      @change="changeFontProperties('fontFamily', fontFamily)"
    >
      <option v-for="(font, i) in fonts" :key="i">{{ font }}</option>
    </select>
  </div>

  <!-- Modify Border -->
  <h3>Modify Border:</h3>
  <p>Change Border Radius</p>
  <input
    type="range"
    v-model="borderRadius"
    min="0"
    max="50"
    @input="this.$refs.businessCard.changeBorderRadius(borderRadius)"
  />
  <p>Change Border Width</p>
  <input
    type="range"
    v-model="borderWidth"
    min="0"
    max="20"
    @input="this.$refs.businessCard.changeBorderWidth(borderWidth)"
  />
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
      borderRadius: 0,
      borderWidth: 0,
      pProperties: { x: 20, y: 100, width: 500, height: 100, rotation: 0 },
      h2Properties: { x: 10, y: 10, width: 200, height: 50, rotation: 0 },
      cardDescriptionActive: true,
      cardHeadingActive: true,
      activeEl: "",
      selectedColor: "",
      fontSize: 20,
      fontFamily: "Poppins",
      fonts: ["Arial", "Poppins", "Serif", "Sans-Serif", "Monospace"],
    };
  },
  methods: {
    changeFontProperties(property, value) {
      let el = document.getElementById(this.activeEl).style;
      switch (property) {
        case "textDecoration":
          el.textDecoration = value;
          break;
        case "fontStyle":
          el.fontStyle = value;
          break;
        case "fontWeight":
          el.fontWeight = value;
          break;
        case "fontSize":
          el.fontSize = `${value}px`;
          break;
        case "fontFamily":
          el.fontFamily = value;
          break;
      }
    },
    deleteActiveEl() {
      document.getElementById(this.activeEl).style.display = "none";
      eval(`this.${this.activeEl}Active = false`);
    },
    toogleActiveAllWrappers(bool) {
      this.cardDescriptionActive = bool;
      this.cardHeadingActive = bool;
    },
    saveCardAsImage(imageFormat) {
      this.toogleActiveAllWrappers(false);
      setTimeout(() => {
        console.log("waiting");
        this.$refs.businessCard.printCard(imageFormat);
        this.toogleActiveAllWrappers(true);
      }, 1000);
    },
    applyBorderColor(){
      this.$refs.businessCard.changeBorderColor(this.selectedColor);
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
        this.selectedColor = instance.toHEXA();
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
