<template>
  <div class="v-carousel-item" :style="{'min-width': width + 'px'}">
    <img v-if="imageSlide" :src="require('../assets/images/' + item_data.img)" alt="item_data.name">
    <div v-else class="item__content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item_data: {
      type: Object,
      default: () => {}
    },
    imageSlide: {
      type: Boolean,
      default: true
    },
    width: {
      type: Number,
      default: 300
    }
  }
}
</script>

<style lang="scss">
// .v-carousel-item {
//   min-width: 300px;
// }
</style>
