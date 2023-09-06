<template>
    <Header/>
    <h1>Hello User, Welcome to Add Page</h1>
    <form class="add">
    <input type="text" placeholder="Enter Name" v-model="restaurant.name">    
    <input type="text" placeholder="Enter Address" v-model="restaurant.address">    
    <input type="text" placeholder="Enter Contact" v-model="restaurant.contact"> 
    <button type="button" v-on:click="addResturant">Add New Resturant</button>   
    </form>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
    name: 'Add',
    components: {
        Header,
    },
    data(){
        return{
        restaurant : {
            name : '',
            address : '',
            contact : ''
        }
        }
    },
    methods:{
      async addResturant(){
            const result = await axios.post('http://localhost:3000/resturant', {
                name : this.restaurant.name,
                address : this.restaurant.address,
                contact : this.restaurant.contact,
            });
            if(result.status == 201){
                this.$router.push({name : 'Home'})
            }
            console.log("result: ", result) 
        }
    },
    mounted()
        {
            let user = localStorage.getItem('user-info')
            if(!user) {
                this.$router.push({name: 'SignUp'})
            }
        }
}
</script>