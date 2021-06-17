<template>
    <div class="card">
        <img v-if="film.poster_path != null" class="poster" :src="this.imgUrl+film.poster_path" alt="">
        <img v-else class="poster" src="../img/noImage.png" alt="">
        <div class="back"></div>
        <div class="info">
            <h2> {{film.original_title}}</h2>
            <h4 v-if="film.original_title != film.title">{{film.title}}</h4>
            <div id="language">
                <img class="flag" v-if="film.original_language == 'it'" src="../img/it.png" alt="it">
                <img class="flag" v-else-if="film.original_language == 'en'" src="../img/en.png" alt="it">
                <h4 v-else>{{film.original_language}}</h4>
            </div>
            <ul v-if="film.vote_average != '' ">
                <li>
                    {{star()}}
                </li>
                <li>
                    <i class="fa-star" :class="{fas : vote >= 0 , far : vote == 0 }"></i>
                </li>
                <li>
                    <i class="fa-star" :class="{fas : vote >= 4 , far: vote < 4 }"></i>
                </li>
                <li>
                    <i class="fa-star" :class="{fas : vote >= 6, far: vote < 6 }"></i>
                </li>
                <li>
                    <i class="fa-star" :class="{fas : vote >= 8 , far: vote < 8 }"></i>
                </li>
                <li>
                    <i class="fa-star" :class="{fas : vote >= 9, far: vote < 9 }"></i>
                </li>
            </ul>
            <p>{{this.film.overview}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardFilm',
    data: function() {
        return {
            vote: ''
        }
    },
    props: {
        film : Object,
        imgUrl : String
    },
    methods : {
        star: function () {
            const vote = Math.round(this.film.vote_average);
            this.vote = vote;

            console.log(this.vote);
        }
    }
}
</script>

<style lang="scss">
    .card {
        position: relative;
        text-align: center;
        width: calc((100% - 120px) / 6);
        height: 450px;
        margin: 10px;
        border: 1px solid black;
        box-shadow: 0 0 10px 5px black;
        cursor: pointer;
        .back,
        .poster {
            width: 100%;
            height: 100%;
            object-fit: cover;
            object-position: center;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%,-50%);
        }

        &:hover .info {
            opacity: 0.9;
        }
        &:hover .back {
            opacity: 0.8;
        }

        ul {
            list-style: none;

            li {
                display: inline-block;
                text-decoration: none;
            }
        }
    }
    .fa-star {
        color: yellow;
    }
    .info{
        opacity: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        padding-top: 20%;
        padding-left: 15px;
        padding-right: 15px;
        height: 400px;
        color: white;

        h2 {
            font-size: 35px;
        }

        .example::-webkit-scrollbar {
            display: none;
        }

        p {
            max-height: 200px;
            overflow: auto;
        }
    }
    .back{
        opacity: 0;
        background-color: black;
    }
    .flag {
        width: 40px;
    }
</style>