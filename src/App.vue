<template>
  <h1>Business Card Generator!</h1>
  <BusinessCard />
</template>

<script setup>
import BusinessCard from "./components/BusinessCard.vue";
components: {
  BusinessCard;
}
</script>

<style>
#app {
  font-family: "Courier New", Courier, monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  flex-direction: column;
  align-items: center;
  color: #2c2c2c;
  margin-top: 60px;
}
</style>
