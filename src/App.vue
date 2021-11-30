<template>
  <h1>Business Card Generator!</h1>
  <!-- Using BusinessCard Component  -->
  <BusinessCard :is-round="isRound" :border-width="borderWidth" />

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
    <i>Dertermines border width</i>
    <p>Border Width: (default 0)</p>
    {{ borderWidth }}
    <select v-model="borderWidth">
      <option
        v-for="option in options"
        :value="option.value"
        :key="option.value"
      >
        {{ option.text }}
      </option>
    </select>
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
      borderWidth: 0,
      options: [
        { text: "0", value: 0 },
        { text: "1", value: 1 },
        { text: "2", value: 2 },
        { text: "3", value: 3 },
      ],
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
