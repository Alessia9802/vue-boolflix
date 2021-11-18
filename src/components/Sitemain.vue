<template>
  <div id="site_main"></div>
  <!-- site_main -->
</template>

<script>
//import axios from "axios";
export default {
  mounted() {
    var axios = require("axios");

    var config = {
      method: "get",
      url: "https://api.themoviedb.org/3/search/movie?api_key=9753c357316b77220b9816dfee198cf6&language=it-IT&query=it&page=1&include_adult=false",
      headers: {},
    };

    axios(config)
      .then(function (response) {
        console.log(JSON.stringify(response.data));
      })
      .catch(function (error) {
        console.log(error);
      });
  },
};
</script>

<style lang="scss"></style>
