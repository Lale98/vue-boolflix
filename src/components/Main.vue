<template>
  <div id="main">
    <SearchBar @searchFilm="searchFilm" @searchTv="searchTv" />
    <h2 :class="{hidden: this.films.length == 0}">Film</h2>
    <div class="film-container">
        <CardFilm :film="film" :imgUrl='imgUrl' v-for="film,index in films" :key='index' />
    </div>
    <h2 :class="{hidden: this.tvs.length == 0}">Serie TV</h2>
    <div class="tv-container">
        <CardTv :tv="tv" :imgUrl='imgUrl' v-for="tv,index in tvs" :key='index' />
    </div>
  </div>
</template>

<script>
import SearchBar from './SearchBar.vue'
import axios from 'axios';
import CardFilm from './CardFilm.vue';
import CardTv from './CardTv.vue';


export default {
    name: 'Main',
    components: { 
        SearchBar,
        CardFilm,
        CardTv
        },
    data: function () {
        return{
            films : [],
            tvs: [],
            imgUrl: 'https://image.tmdb.org/t/p/w342',
            apiFilm: `https://api.themoviedb.org/3/search/movie`,
            apiTv: 'https://api.themoviedb.org/3/search/tv',
            api_key: 'eac04007b3b3652d355621a9c159dfd2',
            query: ''
        }
    },
    methods: {
        searchFilm : function (inputText) {

            this.query = inputText;

            axios
            .get(this.apiFilm, {
                params : {
                    api_key: this.api_key,
                    query: this.query
                }
            })
            .then(
                (element) => {
                    this.query = inputText;
                    this.films = element.data.results;
                    console.log(this.films);
                }
            )
        },
        searchTv : function (inputText) {

            this.query = inputText;

            axios
            .get(this.apiTv, {
                params : {
                    api_key: this.api_key,
                    query: this.query
                }
            })
            .then(
                (element) => {
                    this.query = inputText;
                    this.tvs = element.data.results;
                    console.log(this.tvs);
                }
            )
        },    
    }

}
</script>

<style lang="scss" scoped>
    #main {
        height: 100vh;
        background-color: rgba(black, 0.7);
        overflow: auto;
    }
    .hidden {
        display: none;
    }
    .tv-container,
    .film-container {
        display: flex;
        flex-wrap: wrap;
    }
    h2 {
        font-size: 30px;
    }
</style>