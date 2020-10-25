<template>
  <div class="card-body">
    <h3 class="card-title text-center font-weight-bold">
      {{ meal.strMeal }}
    </h3>
    <p class="card-text recipe overflow-auto text-justify px-2">
      {{ meal.strInstructions }}
    </p>
  </div>
</template>

<script>
export default {
  props: ["meal"]
};
</script>

<style lang="sass" scoped>
.recipe
    max-height: 315px
</style>
