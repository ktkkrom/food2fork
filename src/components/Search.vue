<template lang="html">
<div class="">
  <form>
      <input v-model="recipe"type="text" value="" placeholder="type a word">
      <button type="button" @click="searchRecipe()"name="">Search</button>
  </form>
  <p>page {{currentPage}}</p>
  <button type="button"class="btn-next" :class="buttonColor" @click="fetchNextPage()"name="button">next</button>
  <div v-for="recipe in recipes" :key="recipe.recipeId">
    <Recipe
    :publisher="recipe.publisher"
    :f2fUrl="recipe.f2f_url"
    :title="recipe.title"
    :recipeId="recipe.recipe_id"
    :imageUrl="recipe.image_url"
    :socialRank="recipe.social_rank"
    />
  </div>
</div>
</template>

<script>
import axios from 'axios';
import Recipe from './Recipe.vue';
import {
  required,
  minLength
} from 'vuelidate/lib/validators'

export default {
  name: "Search",
  components: {
    Recipe
  },
  data: () => ({
    recipe: "",
    recipes: [],
    count: 0,
    currentPage: 1,
    token: '7003455ee7fd3683f2b5fea2e6ae90c0'
  }),
  methods: {
    searchRecipe() {
      axios.get(this.searchUrl)
        .then(result => {
          this.count = result.data.count;
          this.recipes = result.data.recipes;
        })
    },
    fetchNextPage() {
      this.currentPage += 1;
      this.searchRecipe();
    }
  },
  computed: {
    searchUrl() {
      return `https://www.food2fork.com/api/search?key=${this.token}&q=${this.recipe}&page=${this.currentPage}`
    },
    buttonColor() {
      if (this.count === 30) {
        return 'btn-active';
      }
      return 'btn-disabled'
    }

  }
}
</script>

<style lang="css" scoped>
.btn-next {
  color: white;
  background-color: green;
  margin-top: 2px;
  width: 100px;
}
.btn-active {
  background-color: green;
}
.btn-disabled {
  background-color: red;
}
</style>
