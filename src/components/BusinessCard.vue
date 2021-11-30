<template>
  <div id="business-card" :class="{ isRound: 'round' }">
    <p>business card</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isRound: true,
    };
  },
};
</script>

<style scoped>
#business-card {
  width: 400px;
  height: 228px;
  box-shadow: -2px 2px 25px 0px rgba(0, 0, 0, 0.4);
  -webkit-box-shadow: -2px 2px 25px 0px rgba(0, 0, 0, 0.4);
  -moz-box-shadow: -2px 2px 25px 0px rgba(0, 0, 0, 0.4);
}
.round {
  border-radius: 7px;
}

@media screen and (max-width: 418px) {
  #business-card {
    background: yellow;
    width: 300px;
    height: 168px;
  }
}
</style>
