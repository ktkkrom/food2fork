<template lang="html">
  <div class="recipe">
    <p> published by {{ publisher }}</p>
    <a :href="f2fUrl"> f2f</a>
    <h2> {{ title }}</h2>
    <img :src="imageUrl" :alt="title" width="100">
    <p>Rank: {{ socialRank }}</p>
  </div>

</template>

<script>
export default {
  name: 'Definition',
  props: {
    publisher: String,
    f2fUrl: String,
    title: String,
    recipeId: String,
    imageUrl: String,
    socialRank: Number
  }
}
</script>

<style lang="css" scoped>
.recipe {
  border: 1px solid green;
}
</style>

<!-- бинд на атрибут -->
