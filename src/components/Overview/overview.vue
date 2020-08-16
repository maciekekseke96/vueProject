<template>
  <div class="overviewSection">
    <h1>Podgląd zamówienia</h1>
    <div class="overview tshirtStateFront">
      <div
        v-if="printPlaces.includes('front')"
        class="choosenImgFront"
        v-bind:style="[this.choosenImgFrontStyle]"
      ></div>
    </div>
    <div class="overview tshirtStateBack">
      <div
        v-if="printPlaces.includes('back')"
        class="choosenImgBack"
        v-bind:style="[this.choosenImgBackStyle]"
      ></div>
    </div>
    <div class="overview currentPrice">
      <p>Cena: {{ this.currentPrice }} zł</p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageID: {
      type: Number,
    },
    printPlaces: {
      type: Array,
    },
  },
  name: "overview",
  data() {
    return {
      currentPrice: 20,
      choosenImgFrontStyle: {
        position: "absolute",
        width: "100px",
        height: "100px",
        border: "1px solid black",
        left: "61px",
        top: "60px",
        backgroundImage: `url("https://picsum.photos/id/${this.imageID}/100/")`,
      },
      choosenImgBackStyle: {
        position: "absolute",
        width: "100px",
        height: "100px",
        border: "1px solid black",
        left: "67px",
        top: "60px",
        backgroundImage: `url("https://picsum.photos/id/${this.imageID}/100/")`,
      },
    };
  },
  created() {
    console.log(this.imageID);
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

.overviewSection {
  height: 100%;
  width: 30%;
  border-left: 2px solid black;
  font-family: "Russo One", sans-serif;
  color: #def2f1;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 30px;
}

.overviewSection h1 {
  text-align: center;
}
.overview {
  margin-top: 10px;
}
.overview.currentPrice {
  width: 230px;
  height: 40px;
  font-size: 30px;
  text-align: right;
}
.overview.tshirtStateFront {
  width: 230px;
  height: 240px;
  border: 1px solid black;
  background-image: url("../../assets/tshirtFront.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  background-position: cover;
  position: relative;
}
.overview.tshirtStateBack {
  width: 230px;
  height: 240px;
  border: 1px solid black;
  background-image: url("../../assets/tshirtBack.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  background-position: cover;
  position: relative;
}
</style>
