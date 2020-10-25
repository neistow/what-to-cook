<template>
  <div class="meal my-5">
    <div class="card">
      <div class="row no-gutters">
        <div class="col-md-12">
          <div class="card-header">
            <nav
              class="nav nav-fill nav-tabs flex-column flex-md-row"
              id="v-pills-tab"
              role="tablist"
              aria-orientation="vertical"
            >
              <a
                v-for="tab in tabs"
                :key="tab"
                class="flex-sm-fill text-sm-center nav-link"
                :class="{ active: currentTab === tab }"
                @click="currentTab = tab"
              >
                {{ tab }}
              </a>
            </nav>
          </div>
        </div>
      </div>
      <div class="row no-gutters">
        <div class="col-md-4 d-flex justify-content-center align-items-center">
          <img
            v-show="isLoaded"
            :src="meal.strMealThumb"
            class="card-img"
            :alt="meal.strMeal"
            @load="onLoaded"
          />
          <div v-if="isLoading" class="spinner-border my-5" role="status">
            <span class="sr-only">Loading...</span>
          </div>
        </div>
        <div class="col-md-8 d-flex align-items-center justify-content-center">
          <component :is="currentTab" :meal="meal"></component>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Recipe from "./Recipe";
import Video from "./Video";
import Ingredients from "./Ingredients";

export default {
  props: ["meal"],
  data() {
    return {
      isLoaded: false,
      isLoading: true,
      tabs: ["Recipe", "Video", "Ingredients"],
      currentTab: "Recipe"
    };
  },
  components: {
    Recipe,
    Video,
    Ingredients
  },
  methods: {
    onLoaded() {
      this.isLoaded = true;
      this.isLoading = false;
    }
  }
};
</script>

<style lang="sass" scoped>
.nav-link
  &:hover
    cursor: pointer !important
</style>
