<template>
  <div class="appMain"></div>
</template>

<script>
import appHeader from "./components/Header/appHeader.vue";
import printPlace from "./components/MainContent/printPlace.vue";
import chooseImage from "./components/MainContent/chooseImage.vue";
import userDataForm from "./components/MainContent/userDataForm.vue";
import orderSummary from "./components/MainContent/orderSummary.vue";
import thankyouPage from "./components/MainContent/thankyouPage.vue";

export default {
  components: {
    appHeader: appHeader,
    printPlace: printPlace,
    chooseImage: chooseImage,
    userDataForm: userDataForm,
    orderSummary: orderSummary,
    thankyouPage: thankyouPage,
  },
  name: "app",
  data() {
    return {
      msg: "Welcome to Your Vue.js App",
    };
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
  border: 1px solid black;
  background-color: #3aafa9;
}
</style>
