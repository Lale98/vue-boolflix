<template>
  <div>
      <input type="text" v-model="inputText" @keyup.enter="$emit('searchFilm', inputText),$emit('searchTv', inputText)">
      <button @click="$emit('searchFilm', inputText),$emit('searchTv', inputText)">Cerca</button>
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  data: function () {
    return {
      inputText : ''
    }
  }
}
</script>

<style lang="scss" scoped>
  div {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 50px;
    background-color: rgba(black, 0.8);
  }
</style>