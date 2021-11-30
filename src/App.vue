<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard ref="businessCard" />

  <!-- Download BusinessCard -->
  <button class="btn" @click="this.$refs.businessCard.saveCardAsImage('png')">
    Download Card As png
  </button>
  <button class="btn" @click="this.$refs.businessCard.saveCardAsImage('jpeg')">
    Download Card As jpeg
  </button>
</template>

<script>
import BusinessCard from "./components/BusinessCard.vue";
export default {
  data() {
    return {};
  },
  components: {
    BusinessCard,
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
  background: rgb(64, 242, 255);
  border: 1px solid rgb(65, 217, 255);
}
.btn.active {
  border: 1px solid rgb(109, 255, 109);
  background: rgb(212, 255, 212);
}
</style>
