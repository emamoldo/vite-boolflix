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
    },
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

  <main id="main_section">
    <section class="main">
      <div class="container_movie">
        <div v-for="movie in moviesList">
          <div class="movies">
            <div>

              <img :src="`https://image.tmdb.org/t/p/w185/${movie.poster_path}`" alt="">

              <div class="info">
                {{ movie.title }}
                {{ movie.original_title }}
                {{ movie.original_language }}
                <img :src="`https://flagsapi.com/${movie.original_language.toUpperCase()}/flat/48.png`" alt="">
                {{ Math.ceil(movie.vote_average / 2) }}
                <!-- <i class="fa-solid fa-star"></i> -->
              </div>

            </div>
          </div>
        </div>
      </div>

      <div class="container_series">
        <div class="col" v-for="serie in tvSeries">
          <div class="series">
            <div>

              <img class="poster" :src="`https://image.tmdb.org/t/p/w185/${serie.poster_path}`" alt="">

              <div class="info">
                {{ serie.original_name }}
                <img :src="`https://flagsapi.com/${serie.origin_country}/flat/48.png`" alt="">
                {{ Math.ceil(serie.vote_average / 2) }}
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

main {
  background-color: gray;
}


.info {
  display: none;
}
</style>
