<template>
  <div class="printPlace">
    <h1 v-on:click="changeAppControler">Check if works :)</h1>
  </div>
</template>

<script>
export default {
  name: "printPlace",
  data() {
    return {};
  },
  methods: {
    changeAppControler: function () {
      this.$emit(`changeAppControler`, 0);
    },
  },
};
</script>

<style scoped>
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
</style>
