<template>
  <div>
      <input type="text" v-model="inputText" @keyup.enter="$emit('search', inputText)">
      <button @click="$emit('search', inputText)">Cerca</button>
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
  }
</style>