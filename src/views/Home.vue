<template>
  <div class="home">
    <HeaderHeyOutfit/>
    <Carousel/>
    <SliderProduct/>

  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderHeyOutfit from '@/components/HeaderHeyOutfit.vue'
import Carousel from '@/components/Carousel.vue'
import SliderProduct from '@/components/SliderProduct.vue'


export default {
  name: 'home',
  components: {
    HeaderHeyOutfit,
    Carousel,
    SliderProduct
  }
}
</script>
