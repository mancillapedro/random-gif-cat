<template>
  <div id="app">
    <h1 v-text="`Random Gif Cat`" />
    <form-search @valuesForm="getGatito" :disabled="disabled" />
    <h3 v-if="disabled" v-text="`Loading...`" />
    <img
      v-if="srcImg"
      :src="srcImg"
      alt="gif gatito"
      :class="{ 'd-none': disabled }"
      @load="disabled = false"
    />
  </div>
</template>

<script>
import FormSearch from "./components/FormSearch.vue";

export default {
  name: "App",
  data() {
    return {
      srcImg: "",
      disabled: false,
    };
  },
  components: {
    FormSearch,
  },
  methods: {
    getGatito(e) {
      this.disabled = true;
      this.srcImg = `https://cataas.com/cat/gif/says/${e.path}`;
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
.d-none {
  display: none;
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
h1 {
  margin-bottom: 2rem;
}
</style>
