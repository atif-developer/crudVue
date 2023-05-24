<template>
<div class="container mt-5">
    <h3>Products For You {{ username }}</h3>
    <div class="row g-2">
        <div class="col-lg-2" v-for="items in list" :key="items.id">
            <div class="card">
                <img :src="items.images[0]" class="card-img-top" alt="...">
                <div class="">
                    <h6 class="mt-2 ms-1">{{ items.title }}</h6>
                    <p class="text-danger ms-1"> $ {{ items.price }}</p>
                    <p class="ms-1"> Rating {{ items.rating }}</p>
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Products',
    data() {
        return {
            list: []
        }
    },
    methods: {
       async getProducts() {
        let user = localStorage.getItem('user-info')
        this.username = JSON.parse(user).username
            if (!user) {
                this.$router.push({
                    name: "Login"
                })
            }
           let res = await axios.get('http://localhost:3000/products')
                console.log(res)
                this.list=res.data
        }
    },
    mounted(){
        this.getProducts()
    }
}
</script>

<style>
.card-img-top{
    height: 180px;
}
</style>
