<template>
  <div id="app" class="container my-5">
    <h1
      class="mt-3 mt-md-0"
      v-b-tooltip.hover.top="'Push the button and find out!'"
    >
      What to cook?
    </h1>

    <Meal v-if="isLoaded" :meal="meal" />
    <div v-show="isLoading" class="spinner-border my-5" role="status">
      <span class="sr-only">Loading...</span>
    </div>

    <button
      :disabled="isLoading"
      class="btn btn-primary"
      @click="getRandomRecipe"
    >
      {{ buttonText }}
    </button>
  </div>
</template>

<script>
import Meal from "@/components/meal/Meal.vue";

export default {
  name: "App",
  components: {
    Meal
  },
  data() {
    return {
      meal: null,
      isLoading: false,
      isLoaded: false
    };
  },
  methods: {
    async getRandomRecipe() {
      this.isLoaded = false;
      this.isLoading = true;

      let response = await fetch(
        "https://www.themealdb.com/api/json/v1/1/random.php"
      );

      let json = await response.json();
      this.isLoaded = true;
      this.isLoading = false;
      this.meal = json.meals[0];
    }
  },
  computed: {
    buttonText() {
      return this.meal === null
        ? "Give me something"
        : "Give me something else";
    }
  }
};
</script>

<style lang="sass">
body, html
  height: 100%
  display: grid

#app
  margin: auto
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center

  h1
    text-align: center

  .spinner-border
    width: 3rem
    height: 3rem

@import "node_modules/bootstrap/scss/bootstrap.scss"
@import "node_modules/bootstrap-vue/src/index.scss"
</style>
