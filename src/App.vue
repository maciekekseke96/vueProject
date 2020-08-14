<template>
  <div>
    <printPlace></printPlace>
    <chooseImage></chooseImage>
    <userDataForm></userDataForm>
    <orderSummary></orderSummary>
    <thankyouPage></thankyouPage>
  </div>
</template>

<script>
import printPlace from "./components/printPlace.vue";
import chooseImage from "./components/chooseImage.vue";
import userDataForm from "./components/userDataForm.vue";
import orderSummary from "./components/orderSummary.vue";
import thankyouPage from "./components/thankyouPage.vue";

export default {
  components: {
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
body {
  background-color: yellow;
}
</style>
