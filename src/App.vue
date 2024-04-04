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
      // API for the flags: https://flagsapi.com/:country_code/:style/:size.png --> CHANGE IN: https://flagsapi.com/:country_code(original_language in caps lock)/:flat/:64.png 
    }
  },

  methods: {
    // For the Movies
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
          this.tvSeries = resp.data.results;
        })
    },
    searchSeries() {
      console.log(this.searchText);
      this.movies(`https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=${this.searchText}`)
    },

    // For the Flags
    // flags(url) {
    //   axios
    //     .get(url)
    //     .then(resp => {
    //       console.log(resp.data.original_language.toUpperCase());
    //       this.languageFlag = resp.data.original_language.toUpperCase();
    //       country_code = original_language.toUpperCase();
    //     })
    // }
  },

  mounted() {
    this.movies('https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=')
    this.series('https://api.themoviedb.org/3/search/tv?api_key=1167e581ec02fa604200a947a803071e&language=&query=')

    // this.flags('https://flagsapi.com/:country_code/:flat/:64.png')
  }
}
</script>


<template>
  <header>
    <div class="searchbox">
      <input type="text" v-model="searchText" @keyup="searchMovies" placeholder="Search Movie">
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
                {{ movie.original_language }}
                <br>
                <!-- {{ movie.poster_path }} need to add to the poster_path the https://image.tmdb.org/t/p/w185 -->
                {{ movie.vote_average }}
                <br>
                <br>

                <div class="col" v-for="serie in tvSeries">
                  <h2>TV Series:</h2>
                  <div class="series">
                    <div>
                      {{ serie.original_name }}
                      <br>
                      {{ serie.original_language }}
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
        </div>
      </div>
    </section>
  </main>
</template>

<style></style>
