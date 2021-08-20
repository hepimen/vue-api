<template>
  <div id="app">
    <div class="container">
      <div class="row header mb-5 p-3">
        <div class="col-lg-12">
          <h2>Quotes Today</h2>
        </div>
      </div>
      <div class="row">
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

      /* --- Using Arrow Function --- */
      .then((response) => (this.quotes = response))
      .catch((error) => {
        if (error.response.status) {
          console.log("Check your API");
          console.log("Error", error.message);
        } else if (error.request) {
          console.log(error.request);
        } else {
          console.log("Error", error.message);
        }
      })
      .finally(() => console.log("Data Loading Complete"));

    /* --- Using Standart Function --- */
    // .then(function (response) {
    //   // handle success
    //   console.log(response);
    // })
    // .catch(function (error) {
    //   // handle error
    //   console.log(error);
    // })
    // .finally(function () {
    //   // handle error
    //   console.log("Data Loading Complete");
    // });
  },
  method: {},
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
