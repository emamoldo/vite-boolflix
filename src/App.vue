<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      moviesList: [],
      searchText: '',
    }
  },

  methods: {
    movies(url) {
      axios
        .get(url)
        .then(resp => {
          console.log(resp.data.results, this.moviesList);
          this.moviesList = resp.data.results;
        })
    },

    searchMovies() {
      console.log(this.searchText);
      this.movies(`https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=${this.searchMovies}`)
    }
  },

  mounted() {
    this.movies('https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=')
  }
}
</script>


<template>
  <header>
    <div class="searchbox">
      <input type="text" v-model="searchText" @keyup="searchMovies" placeholder="Search Movie">
      <button type="button">Search</button>
    </div>
  </header>

  <main>
    <section class="movies">
      <div class="container">
        <div class="row">
          <div class="col" v-for="movies in moviesList">
            <div class="card">
              <div>
                {{ movies.title }}
                {{ movies.original_title }}
                {{ movies.original_language }}
                {{ movies.vote_avarage }}
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<style></style>
