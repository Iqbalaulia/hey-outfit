<template>
  <div class="home">
    <HeaderHeyOutfit/>
    <Carousel/>
    <SliderProduct/>
    <InstaHeyOutfit/>
    <PartnerHeyOutfit/>
    <FooterHeyOutfit/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderHeyOutfit from '@/components/HeaderHeyOutfit.vue'
import Carousel from '@/components/Carousel.vue'
import SliderProduct from '@/components/SliderProduct.vue'
import InstaHeyOutfit from '@/components/InstaHeyOutfit.vue'
import PartnerHeyOutfit from '@/components/PartnerHeyOutfit.vue'
import FooterHeyOutfit from '@/components/FooterHeyOutfit.vue'


export default {
  name: 'home',
  components: {
    HeaderHeyOutfit,
    Carousel,
    SliderProduct,
    InstaHeyOutfit,
    PartnerHeyOutfit,
    FooterHeyOutfit
  }
}
</script>
