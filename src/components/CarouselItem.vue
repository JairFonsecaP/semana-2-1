<template>
  <div :class="image.class">
    <img class="d-block" :src="image.src" alt="Photo of a city" />
  </div>
</template>

<script>
export default {
  name: "CarouselItem",
  props: ["image"],
};
</script>

<style scoped>
img {
    height: 400px !important;
    width: 100%;
}

</style>