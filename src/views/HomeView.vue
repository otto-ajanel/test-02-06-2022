<script setup>
import Login from '@/components/Login.vue'
import NavRoutes from '../components/NavRoutes.vue';
</script>

<template>
<NavRoutes/>
  <main>
<div class="content-home">
  <div class="item-home">
    <img src="../assets/img/joshua-dow-_m_9VlF8eUI-unsplash.jpg" alt=" srcset=">
  </div>
  <div class="item-home">
    <Login />

  </div>

</div>
  </main>
</template>
<style >
img{
  border-radius: 20px;
  width: 550px;
  height: auto;
}
.content-home{
display: flex;


align-items:center;
justify-content:space-around;
}
.item-home{
margin: 0 5%;
}
</style>>

