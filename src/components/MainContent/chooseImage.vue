<template>
  <div class="chooseImage">
    <div class="mainSection">
      <h1>Wybierz swoje idealne zdjęcie</h1>
      <div class="randomImg" v-bind:style="[this.randomImgStyles]">
        <div class="previous imgBtn">Poprzednie zdjęcie</div>
        <div class="next imgBtn" v-on:click="nextRandomImg">Losuj następne</div>
      </div>
      <div class="controlButtons">
        <div class="btn" v-on:click="sendDataToApp(0)">
          Wstecz
        </div>
        <div class="btn" v-on:click="sendDataToApp(2)">
          Dalej
        </div>
      </div>
    </div>
    <overview
      v-bind:imageID="imageID"
      v-bind:printPlaces="printPlaces"
      v-bind:currentPrice="currentPrice"
      v-on:changePrice="changePrice($event)"
    ></overview>
  </div>
</template>

<script>
import overview from "../Overview/overview.vue";

export default {
  props: {
    imageID: {
      type: Number,
    },
    currentPrice: {
      type: Number,
    },
    printPlaces: {
      type: Array,
    },
  },
  name: "chooseImage",
  components: {
    overview: overview,
  },
  data() {
    return {
      randomImgStyles: {
        width: "350px",
        height: "350px",
        border: "1px solid black",
        marginTop: "50px",
        backgroundImage: `url("https://picsum.photos/id/${this.imageID}/350/")`,
      },
    };
  },
  methods: {
    nextRandomImg: function () {
      //this.imageID = Math.floor(Math.random() * 1000);
    },
  },
};
</script>

<style scoped>
.chooseImage {
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

.randomImg {
  width: 350px;
  height: 350px;
  border: 1px solid black;
  margin-top: 50px;
  position: relative;
}

.controlButtons {
  width: 70%;
  height: 10%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 40px;
}

.btn {
  height: 100%;
  width: 25%;
  border: 1px solid black;
  font-family: "Russo One", sans-serif;
  font-size: 20px;
  color: #def2f1;
  background-color: #17252a;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
}

.btn:hover {
  cursor: pointer;
  transform: scale(1.08);
}

.imgBtn {
  width: 40%;
  height: 20%;
  border: 1px solid black;
  font-family: "Russo One", sans-serif;
  font-size: 20px;
  color: #def2f1;
  background-color: #17252a;
  display: flex;
  justify-content: center;
  align-items: center;
  text-transform: uppercase;
  text-align: center;
  position: absolute;
  top: 40%;
}

.imgBtn.previous {
  left: -170px;
}

.imgBtn.next {
  right: -170px;
}
</style>
