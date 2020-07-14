<template>
  <div class="product">
    <HeaderHeyOutfit/>
    <FooterHeyOutfit/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderHeyOutfit from '@/components/HeaderHeyOutfit.vue'
import FooterHeyOutfit from '@/components/FooterHeyOutfit.vue'


export default {
  name: 'product',
  components: {
    HeaderHeyOutfit,
    FooterHeyOutfit
  }
}
</script>
