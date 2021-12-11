<template>
  <div id="app">
    <page-body></page-body>
  </div>
</template>

// Nothing exciting to report here
<script>
import PageBody from "./components/PageBody.vue";

export default {
  name: "App",
  components: {
    PageBody,
  },
};
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: grid;
  place-items: center;
}

</style>
