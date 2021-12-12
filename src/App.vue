<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard
    ref="businessCard"
    :image="backgroundImage"
  >
    <!-- LOGO -->
    <DDR
      @click="activeEl = 'cardLogo'"
      :value="logoProperties"
      :parent="true"
      :active="cardLogoActive"
      :minWidth="5"
    >
      <img src="./assets/Vector.png" id="cardLogo" />
    </DDR>

    <!-- HEADING -->
    <DDR
      @click="activeEl = 'cardHeading'"
      :value="headingProperties"
      :parent="true"
      :active="cardHeadingActive"
    >
      <h1 id="cardHeading">HORIZEN</h1>
    </DDR>

    <!-- LOGO -->
    <DDR
      @click="activeEl = 'cardSlogan'"
      :value="sloganProperties"
      :parent="true"
      :active="cardSloganActive"
    >
      <h3 id="cardSlogan">Organic Tea For Healthy People.</h3>
    </DDR>

    <!-- EMAIL -->
    <DDR
      @click="activeEl = 'cardEmail'"
      :value="emailProperties"
      :parent="true"
      :active="cardEmailActive"
    >
      <h3 id="cardEmail">Email: horizen@gmail.com</h3>
    </DDR>

    <!-- PHONE -->
    <DDR
      @click="activeEl = 'cardPhone'"
      :value="phoneProperties"
      :parent="true"
      :active="cardPhoneActive"
    >
      <h3 id="cardPhone">Phone: +01 8283384282</h3>
    </DDR>

    <!-- ADDRESS -->
    <DDR
      @click="activeEl = 'cardAddress'"
      :value="addressProperties"
      :parent="true"
      :active="cardAddressActive"
    >
      <h3 id="cardAddress">Address: 122 Main Street, City, STATE, 00123</h3>
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

    <p>Font Size (number)</p>
    <input
      @change="changeFontProperties('fontSize', fontSize)"
      type="number"
      placeholder="font-size"
      v-model="fontSize"
      min="4"
    />
    <br />
    <p>Selected Elements Width:</p>
    <input
      @change="changeActiveElWidth(activeElWidth)"
      type="number"
      placeholder="width (px)"
      v-model="activeElWidth"
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
  
  <!-- Github Link -->
  <p><strong>Github: https://github.com/simarbagga401/business-card-generator </strong></p>
</template>

<script>
import BusinessCard from "./components/BusinessCard2.vue";
import backgroundImage from "./assets/background.jpg";
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
      backgroundImage:backgroundImage,
      borderRadius: 0,
      borderWidth: 0,
      sloganProperties: { x: 230, y: 110, width: 300, height: 30, rotation: 0 },
      headingProperties: {
        x: 230,
        y: 60,
        width: 200,
        height: 50,
        rotation: 0,
      },
      logoProperties: { x: 170, y: 60, width: 50, height: 50, rotation: 0 },
      emailProperties: { x: 230, y: 190, width: 300, height: 30, rotation: 0 },
      phoneProperties: { x: 230, y: 220, width: 300, height: 30, rotation: 0 },
      addressProperties: {
        x: 230,
        y: 250,
        width: 300,
        height: 50,
        rotation: 0,
      },
      cardSloganActive: true,
      cardHeadingActive: true,
      cardLogoActive: true,
      cardEmailActive: true,
      cardPhoneActive: true,
      cardAddressActive: true,
      activeEl: "",
      selectedColor: "",
      fontSize: 20,
      activeElWidth:50,
      fontFamily: "Poppins",
      fonts: ["Arial", "Poppins", "Serif", "Sans-Serif", "Monospace"],
    };
  },
  methods: {
    changeActiveElWidth(width){
      let el = document.getElementById(this.activeEl).style;
      el.width = `${width}px`
    },
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
    toogleActiveWrappers(bool) {
      this.cardSloganActive = bool;
      this.cardHeadingActive = bool;
      this.cardLogoActive = bool;
      this.cardEmailActive = bool;
      this.cardPhoneActive = bool;
      this.cardAddressActive = bool;
    },
    saveCardAsImage(imageFormat) {
      this.toogleActiveWrappers(false);
      setTimeout(() => {
        console.log("waiting");
        this.$refs.businessCard.printCard(imageFormat);
        this.toogleActiveWrappers(true);
      }, 1000);
    },
    applyBorderColor() {
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
    // console.log(backgroundImage)
    // console.log(this.backgroundImage)
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

/* Css for Cards innercontent */
#cardHeading {
  font-size: 45px;
  color: #6e9a5a;
  transform: translateY(-40px);
}

#cardSlogan,
#cardEmail,
#cardPhone,
#cardAddress {
  transform: translateY(-20px);
}
#cardSlogan {
  color: #3f3f3f;
  font-weight: normal;
}
#cardEmail {
  color: #9a5a5a;
}
#cardPhone {
  color: #9a5a5a;
  font-weight: normal;
}
#cardAddress {
  color: #9a5a5a;
  font-weight: normal;
}
</style>
