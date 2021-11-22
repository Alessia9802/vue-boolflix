<template>
  <div id="app">
    <div id="site_header">
      <!-- navigation bar -->
      <nav>
        <div class="search_box">
          <input
            type="text"
            placeholder="cerca un film"
            v-model="searchString"
          />
          <button @click="callMovies">Cerca</button>
        </div>
      </nav>
    </div>
    <!-- site_header -->
    <div id="site_main">
      <div class="movies">
        <h1>Film</h1>
        <div class="movie" v-for="movie in movies" :key="movie.id">
          <!-- title -->
          <div class="title">
            <h1>{{ movie.title }}</h1>
          </div>
          <div class="locandina">
            <img :src="movie.poster_path" alt="" />
          </div>
          <!-- original_title -->
          <div class="original_title">
            {{ movie.original_title }}
          </div>
          <!-- language -->
          <div class="original_language">
            {{ movie.original_language }}
            <country-flag :country="movie.original_language" size="normal" />
          </div>
          <!-- Vote -->
          <div class="vote_average">
            {{ movie.vote_average }}
          </div>
        </div>
      </div>
      <div class="series_tv">
        <h1>Serie tv</h1>
        <div class="tv" v-for="serie in series" :key="serie.id">
          <!-- title -->
          <div class="name">
            <h1>{{ serie.name }}</h1>
          </div>
          <div class="poster">
            <img :src="serie.backdrop_path" alt="" />
          </div>
          <!-- original_title -->
          <div class="original_name">
            {{ serie.original_name }}
          </div>
          <!-- language -->
          <div class="original_language">
            {{ serie.original_language }}
            <country-flag :country="serie.original_language" size="normal" />
          </div>
          <!-- Vote -->
          <div class="vote_average">
            {{ serie.vote_average }}
          </div>
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
import CountryFlag from "vue-country-flag";
//import Siteheader from "./components/Siteheader.vue";
//import Sitemain from "./components/Sitemain.vue";
//import Sitefooter from "./components/Sitefooter.vue";

export default {
  name: "App",
  data() {
    return {
      searchString: "",
      movies_url: "https://api.themoviedb.org/3/search/movie",
      series_url: "https://api.themoviedb.org/3/search/tv",
      image_url: "https://image.tmdb.org/t/p/",
      api_key: "9753c357316b77220b9816dfee198cf6",
      error: null,
      movies: "",
      series: "",
      images: "",
      country: ["it", "en", "de", "fr"],
    };
  },
  methods: {
    callMovies() {
      console.log("cliccato");
      console.log(
        `${this.movies_url}?api_key=${this.api_key}&query=${this.searchString} `
      );
      console.log(
        `${this.series_url}?api_key=${this.api_key}&query=${this.searchString} `
      );
      console.log(
        `${this.image_url}?api_key=${this.api_key}&query=${this.searchString} `
      );
      const full_url = `${this.movies_url}?api_key=${this.api_key}&query=${this.searchString} `;
      const full_url_series = `${this.series_url}?api_key=${this.api_key}&query=${this.searchString} `;
      const poster_url = `${this.image_url}?api_key=${this.api_key}&query=${this.searchString} `;
      axios
        .get(full_url)
        .then((resp) => {
          console.log(resp);
          this.movies = resp.data.results;
        })
        .catch((error) => {
          console.log(error);
          this.error = error;
        });
      axios
        .get(full_url_series)
        .then((resp) => {
          console.log(resp);
          this.series = resp.data.results;
        })
        .catch((error) => {
          console.log(error);
          this.error = error;
        });
      axios
        .get(poster_url)
        .then((resp) => {
          console.log(resp);
          this.images = resp.data.results;
        })
        .catch((error) => {
          console.log(error);
          this.error = error;
        });
    },
  },
  components: { CountryFlag },
};
</script>

<style lang="scss">
@import "./assets/scss/common.scss";
.search_box {
  padding: 1rem;
}
</style>
