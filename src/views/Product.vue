<template>
    <div class="product">
        <HeaderHeyOutfit />
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
                                <div class="product-thumbs" v-if="productDetails.galleries.length > 0">
                                    <carousel class="product-thumbs-track ps-slider" :items="3" :nav="false"
                                        :dots="false">

                                        <!-- menampilkan gambar product ketika diklik -->
                                        <div v-for="imageProduct in productDetails.galleries" :key="imageProduct.id"
                                            class="pt" @click="changeImage(imageProduct.photo)"
                                            :class="imageProduct.photo == photoProduct ? 'active' : '' ">
                                            <img :src="imageProduct.photo" alt="" />
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
                                        <p v-html="productDetails.description"></p>

                                        <h4>${{ productDetails.price}}</h4>
                                    </div>
                                    <div class="quantity">
                                        <a @click="saveKeranjang(productDetails.id)" href="#"
                                            class="primary-btn pd-cart">Add To Cart </a>
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
        <ProductRelate />
        <!-- Product Relate End -->
        <FooterHeyOutfit />
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
        data() {
            return {
                photoProduct: '',
                // menampilkan halaman detail berdsarkan id yang dilempar pada url [0]
                productDetails: [],
                // menyimpan pada local storage[0]
                keranjangUser: []
            }
        },
        methods: {
            changeImage(urlImage) {
                this.photoProduct = urlImage;
            },

            setDataPicture(data) {

                // replace data object productDetails dengan data dari API
                this.productDetails = data;

                // replace value gambar default dengan data dari API galleries
                this.photoProduct = data.galleries[0].photo;

            },

            // menyimpan pada local storage[2]
            saveKeranjang(idProduct) {
                this.keranjangUser.push(idProduct);
                const parsed = JSON.stringify(this.keranjangUser);
                localStorage.setItem('keranjangUser', parsed);
            }

        },

        // menampilkan halaman detail berdsarkan id yang dilempar pada url [1]
        mounted() {

            // menyimpan pada local storage[1]
            if (localStorage.getItem('keranjangUser')) {
                try {
                    this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
                } catch (e) {
                    localStorage.removeItem('keranjangUser');
                }
            }

            axios
                .get("http://shayna-backend.belajarkoding.com/api/products", {
                    params: {
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
    .product-thumbs .pt {
        margin-right: 14px;
    }
</style>