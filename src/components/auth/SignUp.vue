<template>
    <div class="container">
        <h1>SignUp component</h1>
        <div class="mb-3">
            <label for="exampleInputName1" class="form-label">User Name</label>
            <input type="text" class="form-control" id="exampleInputName1" name="username" v-model="username">
        </div>
        <div class="mb-3">
            <label for="exampleInputfirst_name1" class="form-label">First Name</label>
            <input type="text" class="form-control" id="exampleInputfirst_name1" name="first_name" v-model="first_name">
        </div>
        <div class="mb-3">
            <label for="exampleInputlast_name1" class="form-label">Last Name</label>
            <input type="text" class="form-control" id="exampleInputlast_name1" name="last_name" v-model="last_name">
        </div>
        <div class="mb-3">
            <label for="exampleInputContact1" class="form-label">Contact</label>
            <input type="text" class="form-control" id="exampleInputContact1" name="contact" v-model="contact">
        </div>
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
        <button v-on:click="getSignUp()" class="btn btn-primary">SignUp Now</button>
        <RouterLink to="/login">Login</RouterLink>

    </div>
</template>
    
<script>
import axios from 'axios';
export default {
    name: 'SignUp',
    data() {
        return {
            username: '',
            first_name: '',
            last_name: '',
            contact: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async getSignUp() {
            let res = await axios.post("http://localhost:3000/user", {
                username: this.username,
                first_name: this.first_name,
                last_name: this.last_name,
                contact: this.contact,
                email: this.email,
                password: this.password
            });
             console.log(res)
            // if (res.status == 201) {
            //     localStorage.setItem('user-info', JSON.stringify(res.data))
            //     // this.$router.push({name:'home'})
            // }
            if (res.status == 201) {
                localStorage.setItem('user-info',JSON.stringify(res.data))
                this.$router.push({name:'home'})
            }

        }
    },
    mounted() {
        // let user = localStorage.getItem('user-info')
        // if (user) {
        //     // this.$router.push({name:"home"})
        // }
        let user = localStorage.getItem('user-info')
        if (user) {
            this.$router.push({name:'home'})
        }
    }
}
</script>
    
<style></style>
    