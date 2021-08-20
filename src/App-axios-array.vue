<template>
  <div id="app">
    <div class="container">
      <div class="row header mb-5 p-3">
        <div class="col-lg-12">
          <h2>Quotes Today</h2>
        </div>
      </div>
      <div class="row">
        <!-- <p v-for="quote in quotes" v-bind:key="quote._id">
          {{ quote.content }}
        </p> -->
        <ul>
          <li
            v-for="quote in quotes"
            v-bind:key="quote.id"
            v-text="quote.title"
          ></li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
// if Array
import axios from "axios";
import "bootstrap/dist/css/bootstrap.css";

export default {
  name: "app",
  components: {},
  data() {
    return {
      quotes: null,
    };
  },
  mounted() {
    axios
      .get("https://jsonplaceholder.typicode.com/users/1/todos")
      // .then((response) => console.log(response));
      .then((response) => (this.quotes = response.data));
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
.header {
  background: #c0392b;
  color: #fff;
}
</style>
