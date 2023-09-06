<template>
    <Header/>
    <h1>Hello {{ name }}, Welcome to Home Page</h1>
    <table border="1px">
        <tr>
            <td>ID</td>
            <td>Name</td>
            <td>Contact</td>
            <td>Address</td>
            <td>Actions</td>

        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{item.id}}</td>
            <td>{{item.name}}</td>
            <td>{{item.contact}}</td>
            <td>{{item.address}}</td>
            <td><RouterLink :to="'/update/'+item.id">Update</RouterLink></td>
            <button @click="deleteRestaurant(item.id)">Delete</button>
        </tr>
    </table>
</template>

<script>
import axios from 'axios';
import Header from './Header.vue';
export default {
    name: 'Home',
    data() {
        return{
            name: '',
            restaurant: [],
        }
        
    },
    components: {
        Header,
    },

    methods:{
       async deleteRestaurant(id){
            let result = await axios.delete('http://localhost:3000/resturant/'+id);
            if(result.status == 200) {
                this.loadData()
            }
        }, 
        async loadData() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name;
            if(!user) {
                this.$router.push({name: 'SignUp'})
            }

            let result = await axios.get('http://localhost:3000/resturant');
            this.restaurant = result.data;
        }
    },
   async mounted()
        {
            this.loadData()
        }
}
</script>

<style>
table{
    width: 500px;
}
</style>
