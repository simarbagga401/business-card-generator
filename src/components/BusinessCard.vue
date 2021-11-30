<template>
  <div id="business-card" ref="card">
    <h2>business card</h2>
    <p>
      Lorem ipsum dolor sit amet consectetur, adipisicing elit. Eligendi, quas?
    </p>
  </div>
</template>

<script>
export default {
  methods: {
    async saveCardAsImage(imageFormat) {
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
