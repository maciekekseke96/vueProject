<template>
  <div class="printPlace">
    <div class="mainSection">
      <h1>Zaznacz miejsce nadruku na koszulce</h1>
      <div class="placeOptions">
        <div class="option front">
          <h2>Przód</h2>
          <div class="img front"></div>
          <input type="checkbox" value="front" v-model="printPlaces" />
        </div>
        <div class="option back">
          <h2>Tył</h2>
          <div class="img back"></div>
          <input type="checkbox" value="back" v-model="printPlaces" />
        </div>
      </div>
    </div>
    <overview
      v-bind:imageID="imageID"
      v-bind:printPlaces="printPlaces"
    ></overview>
  </div>
</template>

<script>
import overview from "../Overview/overview.vue";

export default {
  props: {
    imageID: {
      type: "number",
    },
  },
  name: "printPlace",
  components: {
    overview: overview,
  },
  data() {
    return {
      printPlaces: [],
    };
  },
  methods: {
    changeAppControler: function () {
      this.$emit(`changeAppControler`, 0);
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

.printPlace {
  width: 80vw;
  height: 70vh;
  border: 4px solid black;
  margin: 40px auto;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2b7a78;
}

.mainSection {
  height: 100%;
  width: 70%;
  border-right: 2px solid black;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 30px;
}

.mainSection h1 {
  font-family: "Russo One", sans-serif;
  color: #def2f1;
}

.placeOptions {
  width: 80%;
  height: 70%;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  margin-top: 40px;
}

.placeOptions .option {
  width: 40%;
  height: 90%;
  border: 3px solid black;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: "Russo One", sans-serif;
  color: #17252a;
  text-transform: uppercase;
}

.img {
  height: 210px;
  width: 200px;
  border: 1px solid black;
  margin-top: 30px;
}

.img.front {
  background-image: url("../../assets/tshirtFront.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  background-position: cover;
}

.img.back {
  background-image: url("../../assets/tshirtBack.jpg");
  background-size: 100%;
  background-repeat: no-repeat;
  background-position: cover;
}

.option input {
  width: 30px;
  height: 30px;
  margin-top: 20px;
}

.overviewSection {
  height: 100%;
  width: 30%;
  border-left: 2px solid black;
}
</style>
