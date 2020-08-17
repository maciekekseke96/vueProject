<template>
  <div class="chooseImage">
    <div class="mainSection">
      <h1>Wybierz swoje idealne zdjęcie</h1>
      <div class="randomImg" v-bind:style="[this.randomImgStyles]">
        <div class="previous imgBtn" v-on:click="previousImg">
          Poprzednie zdjęcie
        </div>
        <div class="next imgBtn" v-on:click="nextRandomImg">Losuj następne</div>
      </div>
      <div class="controlButtons">
        <div class="btn" v-on:click="sendDataToApp(1)">
          Wstecz
        </div>
        <div class="btn" v-on:click="sendDataToApp(3)">
          Dalej
        </div>
      </div>
    </div>
    <overview
      v-bind:currentImgID="currentImgID"
      v-bind:printPlaces="printPlaces"
      v-bind:currentPrice="currentPrice"
    ></overview>
  </div>
</template>

<script>
import overviewChooseImg from "../Overview/overviewChooseImg.vue";

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
    overview: overviewChooseImg,
  },
  data() {
    return {
      currentImgID: this.imageID,
      randomImgStyles: {},
      goBacks: 0,
      previousImgID: this.imageID,
    };
  },
  methods: {
    changeAppControler: function (controler) {
      this.$emit(`changeAppControler`, controler);
    },
    nextRandomImg: function () {
      this.previousImgID = this.currentImgID;
      this.currentImgID = Math.floor(Math.random() * 1000);
      this.randomImgStyles = {
        width: "350px",
        height: "350px",
        border: "1px solid black",
        marginTop: "50px",
        backgroundImage: `url("https://picsum.photos/id/${this.currentImgID}/350/")`,
      };
      this.goBacks = 0;
    },
    previousImg: function () {
      if (this.goBacks === 0) {
        this.currentImgID = this.previousImgID;
        this.randomImgStyles = {
          width: "350px",
          height: "350px",
          border: "1px solid black",
          marginTop: "50px",
          backgroundImage: `url("https://picsum.photos/id/${this.currentImgID}/350/")`,
        };
        this.goBacks++;
      }
    },
    sendDataToApp: function (controler) {
      this.$emit(`dataSent`, {
        printPlaces: this.printPlaces,
        updatedPrice: this.updatedPrice,
      });
      this.changeAppControler(controler);
    },
  },
  created() {
    this.randomImgStyles = {
      width: "350px",
      height: "350px",
      border: "1px solid black",
      marginTop: "50px",
      backgroundImage: `url("https://picsum.photos/id/${this.currentImgID}/350/")`,
    };
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
