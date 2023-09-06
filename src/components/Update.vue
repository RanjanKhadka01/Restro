<template>
    <Header/>
    <h1>Hello User, Welcome to Update Page</h1>
    <form class="add">
        <input type="text" placeholder="Enter Name" v-model="restaurant.name">    
        <input type="text" placeholder="Enter Address" v-model="restaurant.address">    
        <input type="text" placeholder="Enter Contact" v-model="restaurant.contact"> 
        <button type="button" v-on:click="updateResturant">Update New Resturant</button>   
        </form>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
    name: 'Update',
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
       async updateResturant(){
            const result = await axios.put('http://localhost:3000/resturant/' +this.$route.params.id,{
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact,
            });
            if(result.status == 200)
            {
                this.$router.push({name: 'Home'})
            }
        }
    },


   async mounted()
        {
            let user = localStorage.getItem('user-info')
            if(!user) {
                this.$router.push({name: 'SignUp'})
            }
            const result = await axios.get('http://localhost:3000/resturant/' +this.$route.params.id)
            // console.warn(this.$route.params.id)
            // console.log(result.data)
            this.restaurant = result.data
        }
}
</script>