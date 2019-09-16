<template>
  <div id="app">
    <div class="container">
      <div class="title">
        <h1>Best quotes of the world</h1>
        <input placeholder="Author..." />
      </div>
      <Authors />
      <QuoteContainer :quoteData="dataSource" />
    </div>
  </div>
</template>

<script>
// import HelloWorld from "./components/HelloWorld.vue";
import QuoteContainer from "./components/QuoteContainer.vue";
import Authors from './components/Authors.vue'
import axios from "axios";

export default {
  name: "app",
  components: {
    QuoteContainer,
    Authors
  },
  data() {
    return {
      dataSource: undefined
    };
  },
  mounted() {
    axios.get("http://localhost:3001").then(response => {
      this.dataSource = response.data;
    });
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
body {
    padding: 20px;
}
input {
    height: 20px;
    width: 150px;
    margin-left: auto;
}
.title {
    display: flex;
    align-items: center;
}
.container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.title h1 {
    margin-left: auto;
}
.disabled {
    background: lightgray;
}
</style>
