<script setup>
import { onUpdated, ref, watch } from 'vue';
import router from '../router';
import axios from 'axios';
import Swal from 'sweetalert2'

const email=ref("")
const password=ref("")
const  auth=ref(false)
const token=ref('')
const usuario=ref('')
const urll=ref('')


function apiLogin(data){
  
    axios.post("https://candidates-exam.herokuapp.com/api/v1/auth/login",data).then((data)=>{
    auth.value=true
    token.value=data.data.token
    usuario.value=data.data.usuario
    urll.value=data.data.url
    }).catch((err)=>{
         Swal.fire({
  title: 'Error!',
  text: 'ingrese correctamente la contraseña o el email',
  icon: 'error',
  confirmButtonText: 'intentar de nuevo '
  })
  })
}


function login(e){
  e.preventDefault();
 const user ={
   email:email.value,
   password: password.value
 }
const res=apiLogin(user)
    cleanDataL()
}

  watch(auth,(newAuth,oldAuth)=>{
    if (newAuth) {
      cleanDataL()
      localStorage.setItem('auth',true)
      localStorage.setItem('token',token.value)
      localStorage.setItem('usuario',usuario.value)
      localStorage.setItem('url',urll.value)
      router.replace({
        path:'/usuarios'
      })

    }
  })
 function cleanDataL(){
     email.value =''
     password.value =''
 }

</script>

<template>
<form class="row-auto needs-validation" novalidate>
    <div class="row">
        <h1 >Login</h1>
    </div>
    <div class="row-auto">

        
  <div class="row">
      <label for="inputEmail" class="form-label">Email</label>
    <input 
    v-model="email"
    type="email" class="form-control" id="inputEmail" placeholder="examplegt@gmail.com" required>
  </div>      
  <div class="row">
      <label for="inputPassword2" class="form-label">Password</label>
    <input 
    v-model="password"
    type="password" class="form-control" id="inputPassword2" placeholder="...Password" required>
  </div>
  <div class="row ">
 
      <button type="submit" @click="login" class="btn btn-primary mb-3">L O G I N</button>
  </div>
      </div>
    </form>
</template>

<style >
h1{
  color: rgb(125, 125, 189);
  margin-left: 25%;
}
</style>