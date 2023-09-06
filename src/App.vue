<template>
  <RouterView/>
</template>

<script>
  export default {
    name: 'App',
    components:{
    
}
  }
</script>

<style scoped>
.register input, .login input, .add input{
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