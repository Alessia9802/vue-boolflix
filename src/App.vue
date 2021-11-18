<template>
  <div id="app">
    <div id="site_header">
      <!-- navigation bar -->
      <nav>
        <div class="search_box">
          <input type="text" placeholder="search" />
          <button>Cerca</button>
        </div>
      </nav>
    </div>
    <!-- site_header -->
    <div id="site_main">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        <!-- title -->
        <div class="title">
          {{ movie.title }}
        </div>
        <!-- original_title -->
        <div class="original_title">
          {{ movie.original_title }}
        </div>
        <!-- language -->
        <div class="original_language">
          {{ movie.original_language }}
        </div>
        <!-- Vote -->
        <div class="vote_average">
          {{ movie.vote_average }}
        </div>
      </div>
    </div>
    <!-- site_main -->
    <div id="site_footer"></div>
    <!-- site_footer -->
  </div>
</template>

<script>
import axios from "axios";
//import Siteheader from "./components/Siteheader.vue";
//import Sitemain from "./components/Sitemain.vue";
//import Sitefooter from "./components/Sitefooter.vue";

export default {
  name: "App",
  data() {
    return {
      movies: [],
    };
  },
  mounted() {
    axios
      .get(
        "https://api.themoviedb.org/3/search/movie?api_key=9753c357316b77220b9816dfee198cf6&language=it-IT&query=it&page=1"
      )
      .then((r) => {
        this.movies = r.data.response;
        console.log(r.data);
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  components: {},
};
</script>

<style lang="scss">
@import "./assets/scss/common.scss";
.search_box {
  padding: 1rem;
}
</style>
