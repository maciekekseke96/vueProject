<template>
  <div class="appMain">
    <appHeader></appHeader>
    <transition name="fade" mode="out-in">
      <keep-alive>
        <component
          v-bind:is="appSectionList[appSectionController]"
          v-bind:imageID="imgID"
          v-bind:currentPrice="currentPrice"
          v-bind:printPlaces="printPlaces"
          v-bind:userData="userData"
          v-on:changeAppControler="updateSectionController($event)"
          v-on:dataSent="updateDataPrintPlace($event)"
          v-on:dataSentfromChooseImage="updateDataChooseImage($event)"
          v-on:dataSentfromUserForm="updateDataUserForm($event)"
        ></component>
      </keep-alive>
    </transition>
  </div>
</template>

<script>
import appHeader from "./components/Header/appHeader.vue";
import printPlace from "./components/MainContent/printPlace.vue";
import chooseImage from "./components/MainContent/chooseImage.vue";
import userDataForm from "./components/MainContent/userDataForm.vue";
import orderSummary from "./components/MainContent/orderSummary.vue";
import thankyouPage from "./components/MainContent/thankyouPage.vue";
import startingPage from "./components/MainContent/startingPage.vue";

export default {
  components: {
    appHeader: appHeader,
    startingPage: startingPage,
    printPlace: printPlace,
    chooseImage: chooseImage,
    userDataForm: userDataForm,
    orderSummary: orderSummary,
    thankyouPage: thankyouPage,
  },
  name: "app",
  data() {
    return {
      appSectionList: [
        "startingPage",
        "printPlace",
        "chooseImage",
        "userDataForm",
        "orderSummary",
        "thankyouPage",
      ],
      appSectionController: 0,
      printPlaces: [],
      imgID: 0,
      currentPrice: 0,
      userData: {},
    };
  },
  methods: {
    updateSectionController: function (controler) {
      this.appSectionController = controler;
    },
    updateDataPrintPlace: function (data) {
      this.printPlaces = data.printPlaces;
      this.currentPrice = data.updatedPrice;
    },
    updateDataChooseImage: function (data) {
      this.imgID = data.updatedImgID;
    },
    updateDataUserForm: function (data) {
      this.userData = data;
    },
  },
  created() {
    this.imgID = Math.floor(Math.random() * 1000);
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.appMain {
  height: 100vh;
  width: 100vw;
  background-color: #3aafa9;
  padding-top: 15px;
}
.fade-enter-active {
  transition: opacity 1s ease-out;
}
.fade-leave-active {
  transition: opacity 1s ease-out;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
  display: none;
}
</style>
