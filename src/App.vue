<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      moviesList: [],
      searchText: '',
      tvSeries: [],
      languageFlag: [],
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
          // console.log(resp.data.results, this.moviesList);
          this.moviesList = resp.data.results;
        })
    },
    searchMovies() {
      console.log(this.searchText);
      this.movies(`https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=${this.searchText}`)
    },

    // For the Tv Series
    series(url) {
      axios
        .get(url)
        .then(resp => {
          // console.log(resp.data.results, this.tvSeries);

          console.log("serie:", resp.data.results)
          this.tvSeries = resp.data.results;
        })
    },
    searchSeries() {
      console.log(this.searchText);
      this.series(`https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=${this.searchText}`)
    },
  },

  mounted() {
    this.movies('https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=')
    this.series('https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=')
  }
}
</script>


<template>
  <header>
    <div class="searchbox">
      <input type="text" v-model="searchText" @keyup="search" placeholder="Search Movie">
      <button type="button">Search</button>
      <!-- TODO: Use the botton to search the movie -->
    </div>
  </header>

  <main>
    <section class="movies">
      <div class="container">
        <div class="row">
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

                {{ movie.vote_average }}
                <br>
              </div>
            </div>

            <div class="col" v-for="serie in tvSeries">
              <h2>TV Series:</h2>
              <div class="series">
                <div>
                  {{ serie.original_name }}
                  <br>
                  {{ serie.origin_country }}
                  <br>
                  {{ serie.vote_average }}
                  <br>
                  <br>
                </div>
              </div>
            </div>

          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<style></style>
