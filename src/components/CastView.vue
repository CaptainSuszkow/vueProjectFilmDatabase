<template>
  <div class='container'>
        <h3 class='h3 mt-4'>Filmy wg obsady:</h3> <br/>
        <select class="form-control form-control-lg" v-model="selectedCast" @change="changeSelectedCast($event)">
        <option disabled value="">Wybierz obsade</option>
            <option v-for="cast in castList" :value="cast" :key="cast">{{ cast}}</option>
        </select>

  <div v-if="selectedCast">
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
name: 'CastView',
    props: [
        'movies'
    ],
    data: function(){
        return {
            movieList: [],
            castList : [
                ""
            ],
            selectedCast: null,
            show: false
        }
    },
    mounted(){
        for(var movie of this.movies.slice(500,600)){
            for(var cast of movie.cast){
                if(!_.contains(this.castList,cast)){
                    this.castList.push(cast)
                }
            }
        }
    },
    methods: {
    changeSelectedCast( event) {
        this.selectedCast = event.target.options[event.target.options.selectedIndex].text
        this.movieList = _.first(_.filter(this.movies.slice(500,600), (movie)=>{
            if(movie.cast.lenght != 0){
            if( movie.cast.indexOf(this.selectedCast) > -1)
                return true 
            }}),100)
    }
  }
}
</script>

<style>

</style>