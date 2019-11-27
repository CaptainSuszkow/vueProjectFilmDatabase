<template>
  <div id="app" class='container'>
    <h1 class="h1">Baza filmow</h1>
    <Search :movies='movieData' @searchOutput='updateMovies'/>
    <MovieTable :movies='searchedMovies'/>
    <GenresView :movies='movieData'/>
    <CastView :movies='movieData'/>
    <footer class="page-footer font-small blue">

    <!-- Copyright -->
    <div class="footer-copyright text-center py-3">©
        <a>Made by Michał Suszek and Piotr Plichtowski</a>
    </div>
    <!-- Copyright -->

</footer>
  </div>
</template>

<script>
import movies from './assets/movies.json'
import Search from './components/Search.vue'
import MovieTable from './components/MovieTable.vue'
import GenresView from './components/GenresView.vue'
import CastView from './components/CastView.vue'

export default {
  name: 'app',
  components: {
    Search,
    MovieTable,
    GenresView,
    CastView
  },
  data: () =>{
    return {
      movieData: movies,
      searchedMovies: movies
    }
  },
  methods: {
    updateMovies: function(variable) {
      this.searchedMovies = variable
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
