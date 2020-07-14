<template>
  <div class="home">
    <HeaderHeyOutfit/>
    <Carousel/>
   

  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderHeyOutfit from '@/components/HeaderHeyOutfit.vue'
import Carousel from '@/components/Carousel.vue'


export default {
  name: 'home',
  components: {
    HeaderHeyOutfit,
    Carousel
  }
}
</script>
