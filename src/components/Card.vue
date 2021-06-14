<template>
    <div class="card">
        <h2> {{film.original_title}} </h2>
        <h4>{{film.title}}</h4>
        <img class="flag" v-if="film.original_language == 'it'" src="../img/it.png" alt="it">
        <img class="flag" v-else-if="film.original_language == 'en'" src="../img/en.png" alt="it">
        <h4 class="flag" v-else>Lingua Sconosciuta</h4>
        <h4> Voto : {{film.vote_average}} </h4>
    </div>
</template>

<script>
export default {
    name: 'Card',
    props: {
        film : Object
    }
}
</script>

<style lang="scss" scoped>
    .card {
        text-align: center;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        height: 400px;
        margin: 10px;
        padding: 10px;
        width: calc((100% - 120px) / 6);
        border: 1px solid black;
        background-color: blue;
    }
    .flag {
        width: 100px;
    }
</style>