<template>
  <div id="app">
    <div id="site_header">
      <!-- navigation bar -->
      <nav>
        <h1 class="heading">BoolFlix</h1>
        <ul>
          <li><a href="#">Home</a></li>
          <li><a href="#">Serie TV</a></li>
          <li><a href="#">Film</a></li>
          <li><a href="#">Originali</a></li>
          <li><a href="#">Aggiunti di recente</a></li>
          <li><a href="#">La mia lista</a></li>
        </ul>

        <div class="search_box">
          <input
            type="text"
            placeholder="cerca un film"
            v-model="searchString"
          />
          <button @click="callMovies">Cerca</button>
        </div>
        <div class="notifiche">
          <i class="fas fa-bell fa-lg"></i>
          <i class="fas fa-user fa-lg"></i>
        </div>
      </nav>
    </div>
    <!-- site_header -->
    <div id="site_main">
      <h1>Film</h1>
      <div class="movies">
        <div class="movie" v-for="movie in movies" :key="movie.id">
          <div class="locandina">
            <div class="contenuto">
              <!-- original_title -->
              <div class="original_title">
                <h3>{{ movie.original_title }}</h3>
              </div>
              <!-- language -->
              <div
                class="original_language"
                v-if="movie.original_language === 'en'"
              >
                Lingua:
                <country-flag country="gb - ita" size=" normal " />
              </div>
              <div class="original_language" v-else>
                Lingua:
                <country-flag
                  :country="movie.original_language"
                  size="normal"
                />
              </div>
              <!-- Overview -->
              <div class="overview">
                {{ movie.overview }}
              </div>
              <!-- Vote -->
              <div class="vote">
                <p class="vote_text">Voto:</p>
                <div
                  class="vote_average"
                  v-for="index in Math.floor(movie.vote_average / 2)"
                  :key="index"
                >
                  <font-awesome-icon :icon="['fas', 'star']" />
                </div>
                <div
                  class="vote_average_empty"
                  v-for="index in 5 - Math.floor(movie.vote_average / 2)"
                  :key="index"
                >
                  <i class="far fa-star"></i>
                </div>
              </div>
            </div>
            <img
              class="poster"
              v-if="!movie.poster_path === null"
              :src="'https://image.tmdb.org/t/p/w342' + movie.poster_path"
              alt=""
            />

            <img
              class="poster"
              :src="'https://image.tmdb.org/t/p/w342' + movie.poster_path"
              alt=""
              v-else
            />
          </div>
        </div>
      </div>

      <h1>Serie tv</h1>
      <div class="series_tv">
        <div class="tv" v-for="serie in series" :key="serie.id">
          <div class="locandina">
            <div class="contenuto">
              <!-- original_title -->
              <div class="original_name">
                <h3>{{ serie.original_name }}</h3>
              </div>
              <!-- language -->
              <div
                class="original_language"
                v-if="serie.original_language === 'en'"
              >
                Lingua:

                <country-flag country="gb - ita" size=" normal " />
              </div>
              <div class="original_language" v-else>
                Lingua:
                <country-flag
                  :country="serie.original_language"
                  size="normal"
                />
              </div>
              <!-- Overview -->
              <div class="overview">
                {{ serie.overview }}
              </div>
              <!-- Vote -->
              <div class="vote">
                <p class="vote_text">Voto:</p>
                <div
                  class="vote_average"
                  v-for="index in Math.floor(serie.vote_average / 2)"
                  :key="index"
                >
                  <font-awesome-icon :icon="['fas', 'star']" />
                </div>
                <div
                  class="vote_average_empty"
                  v-for="index in 5 - Math.floor(serie.vote_average / 2)"
                  :key="index"
                >
                  <i class="far fa-star"></i>
                </div>
              </div>
            </div>
            <img
              class="poster"
              v-if="serie.poster_path === null"
              :src="'https://image.tmdb.org/t/p/w342' + serie.poster_path"
              alt=""
            />
            <img
              class="poster"
              :src="'https://image.tmdb.org/t/p/w342' + serie.poster_path"
              alt=""
              v-else
            />
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
      //image_url: "https://image.tmdb.org/t/p/342",
      api_key: "9753c357316b77220b9816dfee198cf6",
      error: null,
      movies: "",
      series: "",
      images: "",
      country: ["it", "en", "de", "fr"],
    };
  },
  mounted() {
    //Schermata di anteprima
    axios
      .get(
        "https://api.themoviedb.org/3/search/movie?api_key=9753c357316b77220b9816dfee198cf6&language=it-IT&query=a&page=1&include_adult=false"
      )
      .then((resp) => {
        console.log(resp);
        this.movies = resp.data.results;
      })
      .catch((error) => {
        console.log(error);
        this.error = error;
      });
    axios
      .get(
        "https://api.themoviedb.org/3/search/tv?api_key=9753c357316b77220b9816dfee198cf6&language=it-IT&query=a&page=1"
      )
      .then((resp) => {
        console.log(resp);
        this.series = resp.data.results;
      })
      .catch((error) => {
        console.log(error);
        this.error = error;
      });
  },
  methods: {
    callMovies() {
      /* console.log("cliccato");
      console.log(
        `${this.movies_url}?api_key=${this.api_key}&query=${this.searchString} `
      );
      console.log(
        `${this.series_url}?api_key=${this.api_key}&query=${this.searchString} `
      );
      console.log(
        `${this.image_url}?api_key=${this.api_key}&query=${this.searchString} `
      ); */
      const full_url = `${this.movies_url}?api_key=${this.api_key}&query=${this.searchString} `;
      const full_url_series = `${this.series_url}?api_key=${this.api_key}&query=${this.searchString} `;
      //const poster_url = `${this.image_url}?api_key=${this.api_key}&query=${this.searchString} `;
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
    },
  },
  components: { CountryFlag },
};
</script>

<style lang="scss">
@import "./assets/scss/common.scss";

nav ul > li a {
  text-decoration: none;
  color: white;
  padding-left: 1.5rem;
}

nav ul {
  list-style: none;
  display: flex;
  padding: 1rem;
}

nav {
  background-color: black;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

nav input {
  width: 200px;
  padding: 5px;
  border-radius: 50px;
  border: none;
}

.search_box {
  padding: 1rem;
}

.notifiche {
  color: white;
}

.notifiche i {
  padding: 0.5rem;
}

.heading {
  color: red;
  font-size: 30px;
}

#site_main {
  background-color: rgb(31, 31, 31);
  color: white;
  height: 850px;
}

h1 {
  text-align: center;
  padding: 1rem;
}

button {
  width: 70px;
  padding: 5px;
  border-radius: 20px;
  border: none;
  margin-left: 5px;
  background-color: rgb(71 57 59);
  color: rgb(255 255 255);
  cursor: pointer;
}

.movies .poster,
.series_tv .poster {
  width: 200px;
}

.movies .contenuto,
.series_tv .contenuto {
  padding: 15px;
  z-index: 1;
  position: absolute;
  overflow-y: scroll;
  width: 200px;
  height: 300px;
  background-color: rgba(0, 0, 0, 0.726);
  visibility: hidden;
}

.movie:hover .contenuto,
.tv:hover .contenuto {
  visibility: visible;
}

.movies,
.series_tv {
  display: flex;
  //flex-wrap: wrap;
  overflow-x: scroll;
  width: 1400px;
  margin-left: 3rem;
}

.movies .locandina,
.series_tv .locandina {
  width: 200px;
  height: 300px;
  position: relative;
  z-index: 0;
  margin: 10px;
}

/* .series_tv .locandina > .poster {
  width: 200px;
  //padding: 0.5rem;
} */

.overview {
  font-size: 12px;
  padding-bottom: 10px;
}

.original_language {
  display: flex;
  align-items: center;
}

.vote {
  display: flex;
  color: rgb(255, 217, 0);
}
.vote_text {
  color: white;
}

/* .original_title,
.original_language,
.overview,
.vote_average_empty,
.vote_average {
  display: none;
} */

//scrollbar
/* width */
::-webkit-scrollbar {
  width: 6px;
  height: 6px;
}

/* Track */
::-webkit-scrollbar-track {
  box-shadow: inset 0 0 20px white;
  border-radius: 10px;
}

/* Handle */
::-webkit-scrollbar-thumb {
  background: rgb(204, 7, 7);
  border-radius: 10px;
}
</style>
