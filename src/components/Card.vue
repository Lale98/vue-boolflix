<template>
    <div class="card">
        <h2> {{film.original_title}} </h2>
        <h4>{{film.title}}</h4>
        <h4> Lingua Originale : {{film.original_language}} </h4>
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
        justify-content: space-evenly;
        height: 400px;
        margin: 10px;
        padding: 10px;
        width: calc((100% - 120px) / 6);
        border: 1px solid black;
        background-color: blue;
    }
</style>