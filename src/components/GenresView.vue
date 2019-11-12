<template>
  <div class='container mt-4'>
        <h3 class='h3'>Filmy wg gatunku:</h3> <br/>
        <select class="form-control form-control-lg" v-model="Genre" @change="changeSelectedGenre($event)">
        <option disabled value="">Wybierz gartunek</option>
            <option v-for="genre in genresList" :value="genre" :key="genre">{{ genre}}</option>
        </select>
       

  <div v-if="Genre">
        <table class="table table-bordered mt-5" display='block' overflow-x='auto' v-if="movieList">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Year</th>
                    <th>Cast</th>
                    <th>Genres</th>
                    <!-- and so on -->
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item, idx) in movieList" v-bind:key='idx'>
                    <td>{{item.title}}</td>
                    <td>{{item.year}}</td>
                    <td>{{item.cast.join(',')}}</td>
                    <td>{{item.genres.join(',')}}</td>
                    <!-- and so on -->
                </tr>
            </tbody>
        </table>
  </div>
  </div>
</template>

<script>
import _ from 'underscore'
export default {
name: 'GenresView',
    props: [
        'movies'
    ],
    data: function(){
        return {
            movieList: [],
            genresList : [
                ""
            ],
            Genre: '',
            selectedGenre: null,
            show: false
        }
    },
    mounted(){
        for(var movie of this.movies){
            for(var genre of movie.genres){
                if(!_.contains(this.genresList,genre)){
                    this.genresList.push(genre)
                }
            }
        }
    },
    methods: {
    changeSelectedGenre( event) {
        this.show = true
        this.selectedGenre = event.target.options[event.target.options.selectedIndex].text
        this.movieList = _.first(_.filter(this.movies, (movie)=>{
            if(movie.genres.join(' ').indexOf(this.selectedGenre) > -1)
            return true
            }),100)
    }
  }
}
</script>

<style>

</style>