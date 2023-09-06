<template>
    <div class="register">
        <h2>Sign Up Form</h2>
        <input type="text" v-model="name" placeholder="Enter Name"/>
        <input type="email" v-model="email" placeholder="Enter Email"/>
        <input type="password" v-model="password" placeholder="Enter Password"/>
        <button @click="signUp">Register</button>
        <p>
            <router-link to="/login">Login</router-link>
        </p>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name: 'SignUp',
        data(){
            return{
                name: '',
                email: '', 
                password: '',
            }
        },
        methods:{
           async signUp(){
                let result = await axios.post('http://localhost:3000/users',{
                    name: this.name,
                    email: this.email,
                    password: this.password
                });
                if(result.status == 201){
                    localStorage.setItem('user-info', JSON.stringify(result.data))
                    this.$router.push({name:'Home'})
                }
            }
        },
        mounted()
        {
            let user = localStorage.getItem('user-info')
            if(user) {
                this.$router.push({name: 'Home'})
            }
        }
        
    }
</script>

<style scoped>
.register input {
    display: block;
    width: 350px;
    height: 50px;
    margin-bottom: 15px;
    border: 2px solid rgb(23, 147, 25);
}
button{
    width: 150px;
    height: 50px;
    border: 2px solid rgb(23, 147, 25);
}
</style>