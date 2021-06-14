<template>
  <div id="main">
      <SearchBar @search="search"/>
      <div class="cards-container">
        <Card :film="film" v-for="film,index in films" :key='index' />
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
        apiUrlSearchBase: `https://api.themoviedb.org/3/search/movie?api_key=eac04007b3b3652d355621a9c159dfd2&query=`,

        }
    },
    methods: {
        search : function (film) {
            axios
            .get(this.apiUrlSearchBase + film.replace(/\s/g, "%20"))
            .then(
                (element) => {
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
    .cards-container {
        display: flex;
        flex-wrap: wrap;
    }
</style>