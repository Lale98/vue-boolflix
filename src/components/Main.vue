<template>
  <div id="main">
    <SearchBar @search="search"/>
    <h2>Film</h2>
    <div class="film-container">
        <Card :film="film" v-for="film,index in films" :key='index' :class="{hidden : film.media_type != 'movie'}" />
    </div>
    <h2>Serie TV</h2>
    <div class="tv-container">
        <Card :film="film" v-for="film,index in films" :key='index' :class="{hidden : film.media_type != 'tv'}" />
    </div>
  </div>
</template>

<script>
import SearchBar from './SearchBar.vue'
import axios from 'axios';
import Card from './Card.vue';

export default {
    name: 'Main',
    components: { 
        SearchBar,
        Card
        },
    data: function () {
        return{
            films : [],
            api : {
                apiUrlSearchBase: `https://api.themoviedb.org/3/`,
                api_key: 'api_key=eac04007b3b3652d355621a9c159dfd2',
                action: 'search/multi?',
                query: ''
            }
        }
    },
    methods: {
        search : function (inputText) {
            this.api.query = inputText;
            axios
            .get(`${this.api.apiUrlSearchBase}${this.api.action}${this.api.api_key}&query=${this.api.query}`)
            .then(
                (element) => {
                    this.query = inputText;
                    this.films = element.data.results;
                    console.log(this.films);
                }
            )
        }
    }

}
</script>

<style lang="scss" scoped>
    .item {
        height: 400px;
        margin: 10px;
        padding: 10px;
        width: calc((100% - 120px) / 6);
        background-color: blue;
    }
    .tv-container,
    .film-container {
        display: flex;
        flex-wrap: wrap;
    }
    .hidden {
        display: none;
    }
    h2 {
        font-size: 30px;
    }
</style>