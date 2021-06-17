<template>
    <div class="item">
        <img v-if="popularTv.backdrop_path != null" class="poster" :src="this.imgUrl+popularTv.backdrop_path" alt="">
        <img v-else class="poster" src="../img/noImage.png" alt="">
        <div class="back"></div>
        <div class="details">
            <div class="title">
                <h2> {{popularTv.name}}</h2>
            </div>
            <div class="overview">
                <div class="vote">
                    <div id="language">
                        <img class="flag" v-if="popularTv.original_language == 'it'" src="../img/it.png" alt="it">
                        <img class="flag" v-else-if="popularTv.original_language == 'en'" src="../img/en.png" alt="it">
                        <h4 v-else>{{popularTv.original_language}}</h4>
                    </div>
                    <ul v-if="popularTv.vote_average != '' ">
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
                </div>
                <p>{{this.popularTv.overview}}</p>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'CardPopularTv',
    props : {
        popularTv : Object
    },
    data : function () {
        return {
            imgUrl: 'https://image.tmdb.org/t/p/w342',
            vote : ''

        }
    },
    methods : {
        star: function () {
            const vote = Math.round(this.popularTv.vote_average);
            this.vote = vote;

            console.log(this.vote);
        }
    }
}
</script>

<style lang="scss" scoped>
    .title {
        text-align: center;
    }
    .overview {
        width: 100%;
        display: flex;
        justify-content: center;
    }
    .vote {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin-right: 20px;
    }
    .details{
        padding: 0 15px;
        opacity: 0;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-evenly;
        height: 100%;
        color: white;

        h2 {
            font-size: 35px;
        }

        .example::-webkit-scrollbar {
            display: none;
        }

        p {
            max-width: 200px;
            max-height: 100px;
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