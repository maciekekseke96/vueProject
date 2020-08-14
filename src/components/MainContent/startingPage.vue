<template>
  <div class="startingPage">
    <div class="startBtn" v-on:click = "changeAppControler">Zacznijmy !</div>
  </div>
</template>

<script>
export default {
  name: "startingPage",
  data() {
    return {};
  },
  methods: {
    changeAppControler: function () {
      this.$emit(`changeAppControler`, 1);
    },
  },
};
</script>

<style scoped>
.startingPage {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #2b7a78;
}

.startBtn {
  width: 350px;
  height: 150px;
  border-radius: 30%;
  background-color: #17252a;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #feffff;
  text-transform: uppercase;
  font-family: "Russo One", sans-serif;
  font-size: 25px;
}

.startBtn:hover {
  transform: scale(1.15);
  transition: 1s;
  cursor: pointer;
}
</style>
