<template>
  <div class="userDataForm">
    <div class="mainSection"></div>
    <overview
      v-bind:imageID="imageID"
      v-bind:printPlaces="printPlaces"
      v-bind:currentPrice="currentPrice"
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
  name: "userDataForm",
  components: {
    overview: overview,
  },
  data() {
    return {};
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

.userDataForm {
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
</style>
