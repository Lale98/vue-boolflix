<template>
    <div>
        <header>
            <div id="logo-list">
                <a href="main">
                    <img src="https://fontmeme.com/permalink/210616/4bda3b3e90fc32fe9640062b3a8c41db.png" alt="netflix-font" border="0">
                </a>
                <ul>
                    <li>
                        <h4 @click="homeFilm">Film</h4>
                    </li>
                    <li>
                        <h4 @click="homeTv">Serie TV</h4>
                    </li>
                </ul>
            </div>
            <SearchBar @searchFilm="searchFilm" @searchTv="searchTv" />
        </header>
        <div id="main-search" v-if="this.searching == true && this.onlyFilm == false && this.onlyTv == false">
            <h2 :class="{hidden: this.films.length == 0}">Film</h2>
            <div class="film-container">
                <CardFilm :film="film" :imgUrl='imgUrl' v-for="film,index in films" :key='index' />
            </div>
            <h2 :class="{hidden: this.tvs.length == 0}">Serie TV</h2>
            <div class="tv-container">
                <CardTv :tv="tv" :imgUrl='imgUrl' v-for="tv,index in tvs" :key='index' />
            </div>
        </div>
        <div id="main-popular" v-else-if="this.searching == false && this.onlyFilm == false && this.onlyTv == false">
            <h2>Film Popolari</h2>
            <div class="popular-container">
                <CardPopular :popular="popular" v-for="popular,index in populars" :key="index" />
            </div>
        </div>
        <div id="main-popular-tv" v-else-if="this.searching == false && this.onlyFilm == false && this.onlyTv == true">
            <h2>Serie TV Popolari</h2>
            <div class="popular-tv-container">
                <CardPopularTv :popularTv="popularTv" v-for="popularTv,index in popularTvs" :key="index" />
            </div>
        </div>
    </div>
</template>

<script>
import SearchBar from './SearchBar.vue'
import axios from 'axios';
import CardFilm from './CardFilm.vue';
import CardTv from './CardTv.vue';
import CardPopular from './CardPopular.vue';
import CardPopularTv from './CardPopularTv.vue';


export default {
    name: 'Main',
    components: { 
        SearchBar,
        CardFilm,
        CardTv,
        CardPopular,
        CardPopularTv
        },
    data: function () {
        return{
            onlyTv : false,
            onlyFilm : false,
            searching : false,
            popularTvs: [],
            populars : [],
            films : [],
            tvs: [],
            videoFilms : [],
            apiFilmVideo: 'https://api.themoviedb.org/3/movie/',
            apiPopular: 'https://api.themoviedb.org/3/movie/popular',
            apiPopularTv: 'https://api.themoviedb.org/3/tv/popular',
            imgUrl: 'https://image.tmdb.org/t/p/w342',
            apiFilm: `https://api.themoviedb.org/3/search/movie`,
            apiTv: 'https://api.themoviedb.org/3/search/tv',
            api_key: 'eac04007b3b3652d355621a9c159dfd2',
            query: ''
        }
    },
    created : function () {
        axios
            .get(this.apiPopular, {
                params : {
                    api_key: this.api_key,
                    language : 'it-IT'
                }
            })
            .then(
                (element) => {
                    this.populars = element.data.results;
                    console.log(this.populars);
                }
            )
        axios
            .get(this.apiPopularTv, {
                params : {
                    api_key: this.api_key,
                    language : 'it-IT'
                }
            })
            .then(
                (element) => {
                    this.popularTvs = element.data.results;
                    console.log(this.popularTvs);
                }
            )
    },
    methods: {
        
        searchFilm : function (inputText) {

            this.query = inputText;
            this.searching = true;
            this.onlyTv = false;
            this.onlyFilm = false;
            
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
        homeFilm : function () {
            this.searching = false;
            this.onlyTv = false;

        },
        homeTv : function () {
            this.searching = false;
            this.onlyTv = true;
        }
    }

}
</script>

<style lang="scss" scoped>
@import '../style/style.scss';
    header {
        padding: 0 25px;
        display: flex;
        justify-content: space-between;
        align-items: center;
        height: 80px;
        background-color: $secondaryColor;

        a {
            height: 100%;
            display: flex;
            align-items: center;
        }

        img {
            height: 70%;
        }
    }
    #main-popular-tv h2,
    #main-popular h2 {
        margin-top: 0;
    }
    #main-popular-tv,
    #main-popular {
        padding: 0 25px;
        height: calc(100vh - 80px);
        background-color: $mainColor;
        overflow: auto;
    }
    #main-search {
        padding: 25px;
        height: calc(100vh - 80px);
        background-color: $mainColor;
        overflow: auto;
    }
    #logo-list {
        color: rgba(white, 0.6);
        height: 100%;
        display: flex;
        align-items: center;
    }
    .hidden {
        display: none;
    }
    .popular-tv-container,
    .popular-container,
    .tv-container,
    .film-container {
        display: flex;
        flex-wrap: wrap;
    }
    h2 {
        color: rgba(white, 0.6);
        text-transform: uppercase;
        font-size: 30px;
        margin-top: 45px;
        margin-left: 10px;
    }
    ul {
        margin-left: 80px;
        list-style: none;

        li {
            margin-right: 30px;
            display: inline-block;  
            text-decoration: none;
            cursor: pointer;

            &:hover {
                color: white;
            }
        }
    }
</style>