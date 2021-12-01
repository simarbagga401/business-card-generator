<template>
  <div class="movable-box">
    <h2>movable box</h2>
    <p>
      Lorem ipsum dolor sit, amet consectetur adipisicing elit. Consequatur,
      amet?
    </p>
  </div>
  <DDR v-model="transform" >
    <div style="background: red; width: 100%; height: 100%">
      x={{this.transform.x}}
    </div>
  </DDR>
</template>

<script>
import DDR from "yoyoo-ddr-vue3";
import "yoyoo-ddr-vue3/dist/yoyoo-ddr-vue3.css";
export default {
  components: {
    DDR,
  },
  data() {
    return {
      transform: { x: 100, y: 100, width: 100, height: 100, rotation: 0 },
    };
  },
};
</script>

<style scoped></style>
