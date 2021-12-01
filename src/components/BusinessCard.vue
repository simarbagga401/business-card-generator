<template>
  <div id="business-card" ref="card" contenteditable="">
    <slot></slot>
  </div>
</template>

<script>
export default {
  // TODO: Use domtoimage instead of html2canvas
  methods: {
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
    changeBackground(type, value) {
      if ((type = "color")) this.$refs.card.style.backgroundColor = value;
      if ((type = "image"))
        this.$refs.card.style.backgroundImage = `url(${value})`;
    },
    changeBorderRadius(value) {
      this.$refs.card.style.borderRadius = `${value}px`;
    },
  },
};
</script>

<style scoped>
#business-card {
  width: 400px;
  height: 228px;
  background: rgb(248, 248, 248);
  background-repeat: no-repeat;
  background-size: cover;
  box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  -webkit-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  -moz-box-shadow: 0px 0px 31px 0px rgba(0, 0, 0, 0.15);
  margin: 10px;
  padding: 10px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-sizing: border-box;
  position: relative;
  border: none;
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
