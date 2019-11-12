*eslint-disable no-unused-vars*/

<template>
<div class='container'>
    <form>
        <div class='form-row'>
            <div class="form-group col-md-12">
                <label for="filmTitle">Tytul</label>
                <input type="text" class="form-control" id="filmTitle" placeholder="Tytul" v-model='Title'/>
            </div>
        </div>
        <div class='form-row'>
            <div class="form-group col-md-6">
                <label for="fromProductionDate">Rok produkcji od:</label>
                <input type="number" min='1900' max='2019' class="form-control" id="fromProductionDate" placeholder="liczba naturalna 1900-2019" v-model.number='From'/>
            </div>
            <div class="form-group col-md-6">
                <label for="toProductionDate">Rok produkcji do:</label>
                <input type="number" min='1900' max='2019' class="form-control" id="fromProductionDate" placeholder="liczba naturalna 1900-2019" v-model.number='To'/>
            </div>
        </div>
        <div class='form-row'>
            <div class="form-group col-md-12">
                <label for="cast">Obsada:</label>
                <input type="text" class="form-control" id="cast" placeholder="Obsada" v-model='Cast'/>
            </div>
        </div>
        <input type='button' class='btn btn-primary' @click="search" value='Szukaj'/>
    </form>
</div>
</template>

<script>
import _ from 'underscore'
export default {
    name: 'Search',
    props: [
        'movies'
    ],
    data: function(){
        return {
            Title: '',
            From: '', 
            To: '',
            Cast: ''
        }
    },
    methods:{
        search: function(){
            let output  = this.movies
            output = _.filter(output, (movie) => {
                return movie.title.indexOf(this.Title) > -1
            })
            output = _.filter(output, (movie) => {
                if((this.From == '' || movie.year >= this.From)&&(this.To == '' || movie.year <= this.To))
                return true
            })
            if(this.Cast != ''){
                output = _.filter(output, (movie) => {
                    if( movie.cast.join(' ').indexOf(this.Cast) > -1)
                        return true 
                })
            }
            this.$emit('searchOutput',output)
        }
    }
}
</script>

<style>

</style>