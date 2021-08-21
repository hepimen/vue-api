<template>
  <div id="app">
    <div class="container class-hepimen">
      <div class="row">
        <div class="blockquote-wrapper">
          <div class="blockquote">
            <h1
              v-for="quote in quotes"
              v-bind:key="quote._id"
              v-text="quote.content"
            ></h1>
            <h4
              v-for="quote in quotes"
              v-bind:key="quote._id"
              v-text="quote.author"
            ></h4>
          </div>
        </div>
        <div class="text-center">
          <button class="btn btn-primary" @click="refreshQuote">
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
    this.getQuote();
    // lifecycle = one time access
  },
  methods: {
    getQuote() {
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
    refreshQuote() {
      this.getQuote();
    },
  },
};
</script>

<style>
#app {
  font-family: Marvin Visions Variable, Avenir, Helvetica, Arial, sans-serif;
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
@font-face {
  font-family: "Marvin Visions Variable";
  src: url("https://s3-us-west-2.amazonaws.com/s.cdpn.io/756881/MarvinVisionsTrial-Variable.ttf");
}
body,
html {
  padding: 0;
  margin: 0;
  width: 100%;
  height: 250px;
  background-color: black;
}
.class-hepimen .lead {
  font-size: 2.5rem;
  color: #fff;
}
.class-hepimen .author {
  font-size: 1.5rem;
  color: rgb(255 168 10);
}

/* center the blockquote in the page */
.blockquote-wrapper {
  display: flex;
  padding: 0 20px;
}

/* Blockquote main style */
.blockquote {
  position: relative;
  font-family: "Marvin Visions Variable", sans-serif;
  font-weight: 800;
  color: #ffffff;
  padding: 30px 0;
  width: 100%;
  max-width: 500px;
  z-index: 1;
  margin: 80px auto;
  align-self: center;
  border-top: solid 1px;
  border-bottom: solid 1px;
}

/* Blockquote header */
.blockquote h1 {
  position: relative;
  color: #ffffff;
  font-size: 40px;
  font-weight: 800;
  line-height: 1;
  margin: 0;
}

/* Blockquote right double quotes */
.blockquote:after {
  position: absolute;
  content: "”";
  color: rgba(255, 255, 255, 1);
  font-size: 10rem;
  line-height: 0;
  bottom: -43px;
  right: 30px;
}

/* increase header size after 600px */
@media all and (min-width: 600px) {
  .blockquote h1 {
    font-size: 60px;
  }
}

/* Blockquote subheader */
.blockquote h4 {
  position: relative;
  color: #d3461c;
  font-size: 1.4rem;
  font-weight: normal;
  line-height: 1;
  margin: 0;
  padding-top: 20px;
  z-index: 1;
  margin-bottom: -15px;
}
</style>
