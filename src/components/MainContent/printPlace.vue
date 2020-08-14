<template>
  <h1 v-on:click="changeAppControler">Check if works :)</h1>
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

<style></style>
