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
                                <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                <ul>
                                    <li class="w-icon active">
                                        <a @click="saveKeranjang(itemProduct.id , itemProduct.name , itemProduct.price, itemProduct.galleries[0].photo)" href="#"><i class="icon_bag_alt"></i></a>
                                    </li>
                                    <li class="quick-view">
                                         <router-link v-bind:to="'/product/'+itemProduct.id">+ Quick View </router-link>
                                    </li>
                                </ul>
                            </div>
                            <div class="pi-text">
                                <div class="catagory-name">{{ itemProduct.type }}</div>
                                <router-link v-bind:to="'/product/'+itemProduct.id">
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
            products: [],

            // menyimpan pada local storage[0]
            keranjangUser: []
         };
    },
    methods: {
          // menyimpan pada local storage[2]
            saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct) {

                var productStored = {
                    "id": idProduct,
                    "name": nameProduct,
                    "price": priceProduct,
                    "photo": photoProduct
                }


                this.keranjangUser.push(productStored);
                const parsed = JSON.stringify(this.keranjangUser);
                localStorage.setItem('keranjangUser', parsed);
                // reload page ketika melakukan sesuatu
                window.location.reload();

            }
    },
    // proses axios [1]
    mounted(){

         // menyimpan pada local storage[1]
            if (localStorage.getItem('keranjangUser')) {
                try {
                    this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
                } catch (e) {
                    localStorage.removeItem('keranjangUser');
                }
            }

        axios
        .get("http://shayna-backend.belajarkoding.com/api/products")
        .then(res => (this.products = res.data.data.data))
        // disable eslint
    }
}
</script>

<style scoped>
    .product-item{
        margin-right: 25px;
    }
</style>