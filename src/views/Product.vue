<template>
  <div class="product">
    <HeaderHeyOutfit/>
    <!-- Breadcrumb Section Begin -->
    <div class="breacrumb-section text-left">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="breadcrumb-text product-more">
                        <router-link to="/"><i class="fa fa-home"></i> Home</router-link>
                        <span>Detail</span>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Breadcrumb Section Begin -->

    <!-- Product Shop Section Begin -->
    <section class="product-shop spad page-details">
        <div class="container">
            <div class="row">
                <div class="col-lg-12">
                    <div class="row">
                        <div class="col-lg-6">
                            <div class="product-pic-zoom">
                                <img class="product-big-img" :src="photoProduct" alt="" />
                            </div>
                            <div class="product-thumbs">
                                <carousel class="product-thumbs-track ps-slider" :items="3" :nav="false" :dots="false" >
                                    <div class="pt" @click="changeImage(thumbs[0])" :class="thumbs[0] == photoProduct ? 'active' : '' ">
                                        <img src="img/mickey1.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[1])" :class="thumbs[1] == photoProduct ? 'active' : '' ">
                                        <img src="img/mickey2.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[2])" :class="thumbs[2] == photoProduct ? 'active' : '' ">
                                        <img src="img/mickey3.jpg" alt="" />
                                    </div>

                                    <div class="pt" @click="changeImage(thumbs[3])" :class="thumbs[3] == photoProduct ? 'active' : '' ">
                                        <img src="img/mickey4.jpg" alt="" />
                                    </div>
                                </carousel>
                            </div>
                        </div>
                        <div class="col-lg-6">
                            <div class="product-details text-left">
                                <div class="pd-title">
                                    <span>{{ productDetails.type}}</span>
                                    <h3>{{ productDetails.name}}</h3>
                                </div>
                                <div class="pd-desc">
                                    <p>
                                        {{ productDetails.description  }}
                                    </p>
                                    
                                    <h4>${{ productDetails.price}}</h4>
                                </div>
                                <div class="quantity">
                                     <router-link to="/cart" class="primary-btn pd-cart">Add To Cart</router-link>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
    <!-- Product Shop Section End -->

    <!-- Product Relate -->
    <ProductRelate/>
    <!-- Product Relate End -->
    <FooterHeyOutfit/>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'
import HeaderHeyOutfit from '@/components/HeaderHeyOutfit.vue'
import FooterHeyOutfit from '@/components/FooterHeyOutfit.vue'
import ProductRelate from '@/components/ProductRelate.vue'

import carousel from 'vue-owl-carousel';

import axios from "axios";

export default {
  name: 'product',
  components: {
    HeaderHeyOutfit,
    FooterHeyOutfit,
    carousel,
    ProductRelate
  },
  data(){
      return {
          photoProduct: '',
          thumbs:[
              "img/mickey1.jpg",
              "img/mickey2.jpg",
              "img/mickey3.jpg",
              "img/mickey4.jpg"
          ],
          // menampilkan halaman detail berdsarkan id yang dilempar pada url [0]
          productDetails:[]
      }
  },
  methods: {
      changeImage(urlImage) {
          this.photoProduct = urlImage;
      },
      setDataPicture(data){

        // replace data object productDetails dengan data dari API
        this.productDetails = data;

        // replace value gambar default dengan data dari API galleries
        this.photoProduct = data.galleries[0].photo;

      }
  },
  
  // menampilkan halaman detail berdsarkan id yang dilempar pada url [1]
  mounted(){
        axios
        .get("http://shayna-backend.belajarkoding.com/api/products", {
            params:{
                id: this.$route.params.id
            }
        })
        // set data picture default
        .then(res => (this.setDataPicture(res.data.data)))
        // disable eslint
    }
  
  
}
</script>

<style scoped>
.product-thumbs .pt{
    margin-right: 14px;
}
</style>
