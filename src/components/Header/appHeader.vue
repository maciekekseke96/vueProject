<template>
  <header>
    <div class="uniqueBorderTop"></div>
    <h1>Stwórz swoją unikalną koszulkę</h1>
    <div class="uniqueBorderBottom"></div>
  </header>
</template>

<script>
export default {
  name: "appHeader",
  data() {
    return {};
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Russo+One&display=swap");

@keyframes uniqueBorderTopAnimation {
  0% {
    width: 0%;
  }
  50% {
    width: 100%;
  }
  100% {
    width: 0%;
  }
}

@keyframes uniqueBorderBottomAnimation {
  0% {
    width: 100%;
  }
  50% {
    width: 0%;
  }
  100% {
    width: 100%;
  }
}
header {
  margin: 0 auto;
  width: 80vw;
  height: 80px;
  border-top: 5px solid black;
  border-bottom: 5px solid black;
  display: flex;
  justify-content: center;
  align-items: center;
  color: #feffff;
  text-transform: uppercase;
  font-family: "Russo One", sans-serif;
  font-size: 18px;
  position: relative;
}
.uniqueBorderTop {
  height: 5px;
  width: 0%;
  background-color: #def21f;
  position: absolute;
  top: -5px;
  left: 0;
  animation: uniqueBorderTopAnimation 5s infinite;
}

.uniqueBorderBottom {
  height: 5px;
  width: 100%;
  background-color: #def21f;
  position: absolute;
  bottom: -5px;
  right: 0;
  animation: uniqueBorderBottomAnimation 5s infinite;
}
</style>
