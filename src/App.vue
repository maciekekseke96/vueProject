<template>
  <div class="appMain">
    <appHeader></appHeader>
    <div class="mainContent">
      <component
        v-bind:is="appSectionList[appSectionController]"
        v-on:changeAppControler="updateSectionController($event)"
      ></component>
    </div>
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
    };
  },
  methods: {
    updateSectionController: function (controler) {
      this.appSectionController = controler;
    },
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

.mainContent {
  width: 80vw;
  height: 70vh;
  border: 4px solid black;
  margin: 40px auto;
}
</style>
