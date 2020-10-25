<template>
  <div class="embed-responsive embed-responsive-16by9 video">
    <iframe
      class="embed-responsive-item p-2"
      :src="videoUrl"
      allowfullscreen
    ></iframe>
  </div>
</template>

<script>
export default {
  props: ["meal"],
  computed: {
    videoUrl() {
      let match = this.meal.strYoutube.match(/\?v=(.+)/);
      return match === null
        ? `https://www.youtube.com/embed/dQw4w9WgXcQ`
        : `https://www.youtube.com/embed/${match[1]}`;
    }
  }
};
</script>

<style lang="sass" scoped></style>
