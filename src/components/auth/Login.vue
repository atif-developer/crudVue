<template>
    <div class="container mt-5">
        <h1>Login component</h1>
        <div class="mb-3">
            <label for="exampleInputEmail1" class="form-label">Email address</label>
            <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" name="email"
                v-model="email">
            <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3">
            <label for="exampleInputPassword1" class="form-label">Password</label>
            <input type="password" class="form-control" id="exampleInputPassword1" name="password" v-model="password">
        </div>
        <button v-on:click="getSignUp()" class="btn btn-primary">Login Now</button>
        <RouterLink to="/signUp">SignUp</RouterLink>
    </div>
</template>
    
<script>
import axios from 'axios';
export default {
    name: 'Login',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async getSignUp() {
            let res = await axios.get(`http://localhost:3000/user?email=${this.email}&password=${this.password}`);
            console.log(res)
            // if (res.status == 200 && res.data.length>0) {
            // localStorage.setItem('user-info', JSON.stringify(res.data[0]))
            // this.$router.push({name:'home'})
            // }
            if (res.status == 200 && res.data.length > 0) {
                console.log('successfully')
                localStorage.setItem('user-info',JSON.stringify(res.data[0]))
                this.$router.push({name:'home'})
            }

        }
    },
    mounted() {
        let user = localStorage.getItem('user-info')
        if (user) {
            this.$router.push({name:"home"})
        }
    }
}
</script>
    
<style></style>