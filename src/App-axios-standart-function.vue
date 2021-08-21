<template>
  <div id="app">
    <div class="container-fluid">
      <div class="row">
        <div class="position-absolute top-50 start-50 translate-middle">
          <figure>
            <blockquote class="blockquote">
              <p
                class="lead"
                v-for="quote in quotes"
                v-bind:key="quote._id"
                v-text="quote.content"
              ></p>
            </blockquote>
            <figcaption class="blockquote-footer">
              <p
                v-for="quote in quotes"
                v-bind:key="quote._id"
                v-text="quote.author"
              ></p>
            </figcaption>
          </figure>
          <button class="btn btn-primary" v-on:click="updateQuote">
            New Quote
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// if Object
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
      .get("https://api.quotable.io/random")

      /* --- Using Standart Function --- */
      .then(function (response) {
        // handle success
        console.log(response);
      })
      .catch(function (error) {
        // handle error
        console.log(error);
      })
      .finally(function () {
        // handle error
        console.log("Data Loading Complete");
      });
  },
  methods: {
    updateQuote() {
      alert("TEST");
    },
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
