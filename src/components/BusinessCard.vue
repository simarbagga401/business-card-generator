<template>
  <div id="business-card" ref="card" contenteditable="">
    <h2>business card</h2>

    <DDR
      v-model="transform"
      :parent="true"
      :minWidth="1"
      :active="transformActive"
    >
      <p>
        Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eligendi,
        quas?
      </p>
    </DDR>
  </div>
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
      transform: { x: 100, y: 100, width: 200, height: 100, rotation: 0 },
      transformActive: true,
    };
  },
  methods: {
    saveCardAsImage(imageFormat) {
      this.transformActive = false;
      setTimeout(() => {
        console.log("waiting");
        this.printCard(imageFormat);
        this.transformActive = true;
      }, 1000);
    },
    async printCard(imageFormat) {
      console.log("printing..");
      const el = this.$refs.card;
      const options = {
        type: "dataURL",
      };

      const printCanvas = await html2canvas(el, options);
      const link = document.createElement("a");

      link.setAttribute("download", `download.${imageFormat}`);
      link.setAttribute(
        "href",
        printCanvas
          .toDataURL(`image/${imageFormat}`)
          .replace(`image/${imageFormat}`, "image/octet-stream")
      );
      link.click();
      console.log("done");
    },
    changeBackground(color) {
      this.$refs.card.style.backgroundColor = color;
    },
  },
};
</script>

<style scoped>
#business-card {
  width: 400px;
  height: 228px;
  background: rgb(248, 248, 248);
  border: 1px solid rgb(224, 224, 224);
  box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  border-radius: 30px;
  -webkit-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  -moz-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  margin: 10px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
  position: relative;
}

/* Media-Queries */
@media screen and (max-width: 418px) {
  #business-card {
    width: 300px;
    height: 171px;
  }
}

@media screen and (min-width: 800px) {
  #business-card {
    width: 700px;
    height: 400px;
  }
}
</style>
