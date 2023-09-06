<template>
<div class="nav">
    <RouterLink to="/">Home</RouterLink>
    <RouterLink to="/add">Add Restaurant</RouterLink>
    <!-- <RouterLink to="/update">Update Restaurant</RouterLink> -->
    <a @click="logout" href="#">Logout</a>
</div>
</template>

<script>
export default{
    name: 'Header',
    methods:{
        logout() {
            localStorage.clear();
            this.$router.push({name: 'Login'})
        }
    }
}
</script>

<style>
.nav{
    background-color: #333;
    overflow: hidden;
}
.nav a{
    float: left;
    color: wheat;
    padding: 14px 10px;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}
.nav a:hover{
    background-color: #ddd;
    color: #333;
}

</style>