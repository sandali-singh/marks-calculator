<template>
  <div id="app">
    <calculator></calculator>
  </div>
</template>

<script>
import calculator from "./components/calculator.vue";

export default {
  name: "App",
  components: {
    calculator,
  },
};
</script>

<style scoped>
body {
  margin: 0;
}
#app {
  height: 100vh; /* Take full viewport height */
  background-color: #ccc;
  padding: 0 250px;
  overflow: hidden;
}
</style>
