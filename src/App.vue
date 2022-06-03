<script setup>
import {onMounted, ref} from"vue";
import {  RouterView } from 'vue-router'
import router from './router/index'



localStorage.setItem("auth",false)



onMounted(()=>{
  if (localStorage.getItem("auth")==true) {
    router.replace({
      path:'/usuarios'
    })
  }
})

const auth =ref(localStorage.getItem("auth"));

</script>

<template>
 
<div class="content">
  <RouterView />

</div>
</template>


