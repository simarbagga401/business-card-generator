<template>
  <div id="business-card" :class="{ round: isRound }">
    <p>business card</p>
  </div>
</template>

<script>
export default {
  props: ["isRound"],
  data() {
    return {};
  },
};
</script>

<style scoped>
#business-card {
  width: 400px;
  height: 228px;
  background: rgb(248, 248, 248);
  border: 1px solid rgb(87, 87, 87);
  box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  -webkit-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  -moz-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  margin: 10px;
}

/* Dynamic-Classes */
.round {
  border-radius: 20px;
}

/* Media-Queries */
@media screen and (max-width: 418px) {
  #business-card {
    width: 300px;
    height: 171px;
  }
}

@media screen and (min-width: 1000px) {
  #business-card {
    width: 500px;
    height: 285px;
  }
}
</style>
