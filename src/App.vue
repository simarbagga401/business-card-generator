<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard :isRound="isRound" />

  <!-- Using Options BusinessCard Component Provides -->
  <div id="options">
    <h2>Options:</h2>
    <!-- Option 1  -->
    <i>Determines if Corners of Card are Round.</i>
    <button
      @click="isRound = !isRound"
      class="btn"
      :class="{ active: isRound }"
    >
      Round
    </button>

    <!-- Option 2  -->
    <!-- <i>Dertermines border width</i>
    <button
      @click="isround = !isround"
      class="btn"
      :class="{ active: isround }"
    >
      round
    </button> -->
  </div>
</template>

<script>
import BusinessCard from "./components/BusinessCard.vue";
export default {
  components: {
    BusinessCard,
  },
  data() {
    return {
      isRound: false,
    };
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

#options {
  display: flex;
  flex-direction: column;
}

.btn {
  padding: 5px 10px;
  margin: 5px;
}
.btn.active {
  border: 1px solid rgb(109, 255, 109);
  background: rgb(212, 255, 212);
}
</style>
