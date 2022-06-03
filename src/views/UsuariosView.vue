<script setup>
import Perfil from '../components/Perfil.vue';
import router from '../router';

function logout(){
  localStorage.clear()
  router.replace({
    path:'/'
  })
}
</script>
<template>
    <div class="content-home">
  <div class="item-home">
    <h1>Usuario</h1>
  <Perfil/>

</div>

</div>
<div class="btn-logout">
    <button type="button" 
    @click="logout"
    class="btn-close" aria-label="Close"></button>

</div>
</template>
<style scoped>
.btn-logout{

   top: 0;
   right: 0;
   
   
    position: absolute !important;
    border-radius: 15px;
    font-size: 35px;

}
</style>
