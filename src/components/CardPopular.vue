<template>
    <div class="item">
        <img class="poster" :src="this.imgUrl+popular.backdrop_path" alt="">
        <div class="back"></div>
        <div class="details">
            <h2> {{popular.original_title}}</h2>
            <h4 v-if="popular.original_title != popular.title">{{popular.title}}</h4>
            <div id="language">
                <img class="flag" v-if="popular.original_language == 'it'" src="../img/it.png" alt="it">
                <img class="flag" v-else-if="popular.original_language == 'en'" src="../img/en.png" alt="it">
                <h4 v-else>{{popular.original_language}}</h4>
            </div>
            <ul v-if="popular.vote_average != '' ">
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
            <p>{{this.popular.overview}}</p>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardPopular',
    props : {
        popular : Object
    },
    data : function () {
        return {
            imgUrl: 'https://image.tmdb.org/t/p/w342',
            vote : ''

        }
    },
    methods : {
        star: function () {
            const vote = Math.round(this.popular.vote_average);
            this.vote = vote;

            console.log(this.vote);
        }
    }
}
</script>

<style lang="scss" scoped>
    .details{
        opacity: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        padding-top: 20%;
        padding-left: 15px;
        padding-right: 15px;
        height: 100%;
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
    .item {
        position: relative;
        width: calc((100% - 100px) / 5);
        height: 200px;
        margin: 7px 10px;
        border: 1px solid black;
        box-shadow: 0 0 10px 5px black;

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

        .back{
            opacity: 0;
            background-color: black;
        }
        &:hover .details {
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
</style>