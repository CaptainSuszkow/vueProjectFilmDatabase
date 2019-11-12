<template>
    <div class="container md-10">
        <table class="table table-bordered mt-5" display='block' overflow-x='auto' v-if="data">
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
                <tr v-for="(item, idx) in data" v-bind:key='idx'>
                    <td>{{item.title}}</td>
                    <td>{{item.year}}</td>
                    <td>{{item.cast.join(',')}}</td>
                    <td>{{item.genres.join(',')}}</td>
                    <!-- and so on -->
                </tr>
            </tbody>
        </table>
        <button class="btn btn-success col-2" v-if='listLength < movies.length' @click='listLength += 10'>Pokaz wiecej</button>
        <button class="btn btn-danger col-2" v-if='listLength > 10' @click='listLength -= 10'>Pokaz mniej</button>
        
    </div>
	
</template>

<script>
import _ from 'underscore'

export default {
    name:'MovieTable',
    props:  [
        'movies'
    ],
    data: function(){
        return {
            listLength: 10
        }
    },
    computed: {
        data: function(){
            return _.first(this.movies,this.listLength)
        }
    },
    watch:{
        movies: function(){
            this.listLength = 10;
        }
    }
}
</script>

<style>

</style>