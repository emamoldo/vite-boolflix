<script>
import axios from 'axios';
export default {
  name: 'App',
  data() {
    return {
      moviesList: []
    }
  },
  mounted() {
    axios
      .get('https://api.themoviedb.org/3/search/movie?api_key=1167e581ec02fa604200a947a803071e&query=')
      .then(resp => {
        console.log(resp.data.results);
        this.moviesList = resp.data.results;
      })
  }
}
</script>
<!-- remember to install axios -->


<template>

</template>



<style></style>
