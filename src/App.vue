<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.svg" />
    <Page />
  </div>
</template>

<script>
import Page from "./components/Page.vue";
export default {
  name: "App",
  components: {
    Page: Page,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
img {
  width: 200px
}
</style>
