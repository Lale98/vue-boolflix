<template>
  <div>
      <input type="text" v-model="inputText" @keyup="$emit('searchFilm', inputText),$emit('searchTv', inputText)">
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
  @import '../style/style.scss';
  div {
    height: 100%;
    display: flex;
    align-items: center;
  }
  input {
    background-color: transparent;
    border: 1px solid rgba(white, 0.2);
    height: 40%;
    width: 300px;
    color: white;
    padding: 0 10px;
  }
  button {
    background-color: transparent;
    border: 1px solid rgba(white, 0.2);
    height: 40%;
    color: white;
    padding: 0 10px;
    cursor: pointer;

    &:hover {
      border: 1px solid white;
    }
  }
  
</style>