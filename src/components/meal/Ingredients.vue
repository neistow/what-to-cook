<template>
  <div>
    <ul class="mt-2 mt-md-0">
      <li
        class="text-center"
        v-for="ingredient in ingredients"
        :key="ingredient"
      >
        {{ ingredient }}
      </li>
    </ul>
  </div>
</template>

<script>
import _ from "lodash";

export default {
  props: ["meal"],
  computed: {
    ingredients() {
      let keys = Object.keys(this.meal).filter(
        k => k.match(/str((Measure)|(Ingredient))(\d+)$/) !== null
      );

      return _.zip(keys.slice(0, keys.length / 2), keys.slice(keys.length / 2))
        .filter(kvp => this.meal[kvp[0]] !== "")
        .map(e => `${this.meal[e[0]]} - ${this.meal[e[1]]}`);
    }
  }
};
</script>

<style lang="sass" scoped>
li
  list-style: none
</style>
