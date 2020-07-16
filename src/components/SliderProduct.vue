<template>
    <div>
    <!-- Women Banner Section Begin -->
    <section class="women-banner spad">
        <div class="container-fluid">
            <div class="row">
                
                <div class="col-lg-12 mt-5" v-if="products.length > 0">
                    <carousel class="product-slider" :items="3" :nav="false" :dots="false"  :autoplay="true">
                        
                        <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                            <div class="pi-pic">
                                <img src="/img/mickey1.jpg" alt="" />
                                <ul>
                                    <li class="w-icon active">
                                        <a href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view">
                                         <router-link to="/product">+ Quick View </router-link>
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{ itemProduct.type }}</div>
                                <router-link to="/product">
                                    <h5>{{ itemProduct.name }}</h5>
                                </router-link>
                                <div class="product-price">
                                   {{ itemProduct.price }}
                                    <span>$35.00</span>
                                </div>
                            </div>
                        </div>
                       
                    </carousel>
                </div>

                <div class="col-lg-12 mt-5" v-else>
                    <p>Produk belum tersedia untuk saat ini</p>
                </div>

            </div>
        </div>
    </section>
    <!-- Women Banner Section End -->
    </div>
</template>

<script>
// import owl carousel 
import carousel from 'vue-owl-carousel';
// import axios dari project
import axios from "axios";

export default {
    name: "SliderProduct",
    components:{
        carousel
    },
    // proses axios [0]
    data(){
         return{
            products: []
         };
    },
    // proses axios [1]
    mounted(){
        axios
        .get("http://shayna-backend.belajarkoding.com/api/products")
        .then(res => (this.products = res.data.data.data))
        // disable eslint
        .catch(err => console.log(err));
    }
}
</script>

<style scoped>
    .product-item{
        margin-right: 25px;
    }
</style>