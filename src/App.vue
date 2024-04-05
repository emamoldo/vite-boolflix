<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      moviesList: [],
      searchText: '',
      tvSeries: [],
    }
  },

  methods: {

    // For the Movies
    search() {
      this.searchMovies()
      this.searchSeries()
    },
    movies(url) {
      axios
        .get(url)
        .then(resp => {
          this.moviesList = resp.data.results;
        })
    },
    searchMovies() {
      this.movies(`https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=${this.searchText}`)
    },

    // For the Tv Series
    series(url) {
      axios
        .get(url)
        .then(resp => {
          this.tvSeries = resp.data.results;
        })
    },
    searchSeries() {
      this.series(`https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=${this.searchText}`)
    }
  },
  mounted() {
    this.movies('https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=')
    this.series('https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=')
  },
}
</script>


<template>
  <!-- FontAwesome Cdn -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
    integrity="sha512-DTOQO9RWCH3ppGqcWaEA1BIZOC6xxalwEsw9c2QQeAIftl+Vegovlnee1c9QX4TctnWMn13TZye+giMm8e2LwA=="
    crossorigin="anonymous" referrerpolicy="no-referrer" />

  <header class="header">
    <div class="logo">BOOLFLIX</div>

    <div class="searchbox">
      <input type="text" v-model="searchText" @keyup="search" placeholder="Search Movie">
    </div>
  </header>

  <main>
    <section class="movies">
      <div class="container_movie">
        <h1>Movies:</h1>
        <div v-for="movie in moviesList">
          <div class="movies">
            <div>
              {{ movie.title }}
              <br>

              {{ movie.original_title }}
              <br>

              <img :src="`https://flagsapi.com/${movie.original_language.toUpperCase()}/flat/48.png`" alt="">
              <br>

              {{ movie.original_language }}
              <br>

              <img :src="`https://image.tmdb.org/t/p/w185/${movie.poster_path}`" alt="">
              <br>

              {{ Math.ceil(movie.vote_average / 2) }}
              <!-- <i class="fa-solid fa-star"></i> -->
              <br>
            </div>
          </div>

          <div class="col" v-for="serie in tvSeries">
            <h2>TV Series:</h2>
            <div class="series">
              <div>
                {{ serie.original_name }}
                <br>

                <img :src="`https://flagsapi.com/${serie.origin_country}/flat/48.png`" alt="">
                <br>

                <img :src="`https://image.tmdb.org/t/p/w185/${serie.poster_path}`" alt="">
                <br>
                {{ Math.ceil(serie.vote_average / 2) }}
                <br>
                <br>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<style>
.header {
  height: 50px;
  width: 1870px;
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: center;

  .logo {
    color: red;
    margin: 1rem;
  }

  .searchbox {
    margin: 1rem;
  }
}
</style>
