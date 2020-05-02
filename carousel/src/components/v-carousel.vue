<template>
  <div class="wrapper" :style="{'width': slideWidth + 'px'}">
    <div 
      class="v-carousel"
      :style="{'margin-left': '-' + (100 * currentSlideIndex) + '%' }" 
    >
      <v-carousel-item
        v-for="item in carousel_data"
        :key="item.id"
        :item_data="item"
        :width="slideWidth"
        :imageSlide="true"
      >
        <p>{{item.name}}</p>
        <p>{{item.id}}</p>
      </v-carousel-item>
    </div>
    <button @click="prevSlide">Prev</button>
    <button @click="nextSlide">Next</button>
  </div>
</template>

<script>
import vCarouselItem from "./v-carousel-item";

export default {
  props: {
    carousel_data: {
      type: Array,
      default: () => []
    },
    interval: {
      type: Number,
      default: 0
    },
    slideWidth: {
      type: Number,
      default: 300
    }
  },
  components: {
    vCarouselItem
  },
  data: () => ({
    currentSlideIndex: 0
  }),
  methods: {
    prevSlide() {
      if(this.currentSlideIndex > 0) {
        this.currentSlideIndex--
      } else {
        this.currentSlideIndex = this.carousel_data.length - 1
      }
    },
    nextSlide() {
      if(this.currentSlideIndex >= this.carousel_data.length - 1) {
        this.currentSlideIndex = 0
      } else {
        this.currentSlideIndex++
      }
    }
  },
  mounted() {
    if(this.interval > 0) {
      setInterval(() => {
        this.nextSlide()
      }, this.interval)
    }
  }
}
</script>

<style lang="scss">
  .wrapper {
    width: 300px;
    margin: 0 auto;
    overflow: hidden;
  }

  .v-carousel {
    display: flex;
    transition: all ease .5s;
  }
</style>
