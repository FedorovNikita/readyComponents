<template>
  <div id="app">
    <v-carousel
      :carousel_data="sliderItems"
      :slideWidth="300"
      :interval="3000"
    ></v-carousel>
  </div>
</template>

<script>
import vCarousel from './components/v-carousel'

export default {
  data: () => ({
    sliderItems: [
      {id: 1, name: 'img1', img: '1.jpg'},
      {id: 2, name: 'img2', img: '2.jpg'},
      {id: 3, name: 'img3', img: '3.jpg'},
      {id: 4, name: 'img4', img: '4.jpg'},
      {id: 5, name: 'img5', img: '5.jpg'},
    ]
  }),
  components: {
    vCarousel
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
