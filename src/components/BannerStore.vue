<template>
    <div>
        <!-- Women Banner Section Begin -->
        <section class="women-banner spad">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-lg-12 mt-5" v-if="products.length > 0">
                        <carousel class="product-slider" :items="3" :nav="false" :autoplay="true" :dots="false">
                            <div class="product-item" v-for="itemProduct in products" v-bind:key="itemProduct.id">
                                <div class="pi-pic">
                                    <img v-bind:src="itemProduct.galleries[0].photo" alt="" />
                                    <ul>
                                        <li @click="saveKeranjang(itemProduct.id, itemProduct.name, itemProduct.price, itemProduct.galleries[0].photo)" class="w-icon active">
                                            <a href="#"><i class="icon_bag_alt"></i></a>
                                        </li>
                                        <router-link v-bind:to="'/product/'+itemProduct.id">
                                            <li class="quick-view"><a>+ Quick View</a></li>
                                        </router-link>
                                    </ul>
                                </div>
                                <div class="pi-text">
                                    <div class="catagory-name">{{  itemProduct.type  }}</div>
                                    <a href="#">
                                        <h5>{{  itemProduct.name  }}</h5>
                                    </a>
                                    <div class="product-price">
                                        ${{  itemProduct.price  }}
                                        <span>$35.00</span>
                                    </div>
                                </div>
                            </div>

                        </carousel>
                    </div>
                    <div class="col-lg-12" v-else>
                        <p>
                            Produk terbaru tidak tersedia untuk saat ini
                        </p>
                    </div>
                </div>
            </div>
        </section>
        <!-- Women Banner Section End -->
    </div>
</template>

<script>

import carousel from 'vue-owl-carousel';
import axios from 'axios';
export default {
    name: 'BannerStore',
    components: {
        carousel
    },
    data(){
        return{
            products: [],
            keranjangUser: []
        };
    },
    methods: {
        saveKeranjang(idProduct, nameProduct, priceProduct, photoProduct){

            var productStored = {
                "id" : idProduct,
                "name" : nameProduct,
                "price" : priceProduct,
                "photo" : photoProduct
            }
            this.keranjangUser.push(productStored);
            const parsed = JSON.stringify(this.keranjangUser);
            localStorage.setItem('keranjangUser', parsed);

            window.location.reload();
        }
    },
    mounted() {
        axios
            .get("http://127.0.0.1:8000/api/products")
            .then(res =>(this.products = res.data.data.data))
            .catch(err =>  console.log(err));
        if (localStorage.getItem('keranjangUser')) {
            try {
                this.keranjangUser = JSON.parse(localStorage.getItem('keranjangUser'));
            } catch(e) {
                localStorage.removeItem('keranjangUser');
            }
        }
            
    }
};
</script>

<style scoped>
    .product-item {
        margin-right : 25px;
    }
</style>