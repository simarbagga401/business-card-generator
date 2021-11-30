<template>
  <div id="business-card" :class="dynamicClasses">
    <p>business card</p>
    {{ dynamicClasses }}
    borderWidth: {{ borderWidth }}
  </div>
</template>

<script>
export default {
  props: ["isRound", "borderWidth"],
  data() {
    return {};
  },
  computed: {
    dynamicClasses() {
      // Pushing Dynamic Css Classes in Classes Array and Returning it.
      let Classes = [];
      if (this.isRound) Classes.push("round");
      let borderWidthValue = this.borderWidth;
      Classes.push(`border-${this.borderWidth}`);

      return Classes;
    },
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
#business-card.round {
  border-radius: 20px;
}
#business-card.border-0 {
  outline: 0px solid black;
}
#business-card.border-1 {
  outline: 1px solid black;
}
#business-card.border-2 {
  outline: 2px solid black;
}
#business-card.border-3 {
  outline: 3px solid black;
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
