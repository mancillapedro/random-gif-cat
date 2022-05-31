<template>
  <div id="app">
    <h1>Random Gif Cat</h1>
    <form-search @valuesForm="getGatito" />
  </div>
</template>

<script>
import FormSearch from "./components/FormSearch.vue";

export default {
  name: "App",
  components: {
    FormSearch,
  },
  methods: {
    async getGatito(e) {
      // https://cataas.com/cat/gif/says/holi?filter=sepia&color=orange&size=40
      console.log(e.path);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #add8e6;
  padding-top: 60px;
}
</style>
