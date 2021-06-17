<template>
    <div class="card">
        <img v-if="tv.poster_path != null" class="poster" :src="this.imgUrl+tv.poster_path" alt="">
        <img v-else class="poster" src="../img/noImage.png" alt="">
        <div class="back"></div>
        <div class="info">
            <h2> {{tv.name}}</h2>
            <div id="language">
                <img class="flag" v-if="tv.original_language == 'it'" src="../img/it.png" alt="it">
                <img class="flag" v-else-if="tv.original_language == 'en'" src="../img/en.png" alt="it">
                <h4 v-else>{{tv.original_language}}</h4>
            </div>
            <ul v-if="tv.vote_average != '' ">
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
            <p>{{this.tv.overview}}</p>

        </div>
    </div>
</template>

<script>
export default {
    name: 'CardTv',
    data: function() {
        return {
            vote: ''
        }
    },
    methods : {
        star: function () {
            const vote = Math.round(this.tv.vote_average);
            this.vote = vote;

            console.log(this.vote);
        }
    },
    props: {
        tv : Object,
        imgUrl : String
    }
}
</script>

<style lang="scss" scoped>

</style>