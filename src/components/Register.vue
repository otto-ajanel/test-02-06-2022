<script setup>
 import { onUpdated, ref } from 'vue';
  import axios from 'axios'
import Swal from 'sweetalert2/dist/sweetalert2.js'
import router from '../router';


const nombre =ref("")
const email =ref("")
const password =ref("")
const password_confirmation =ref("")

async function apiRegister(data){
   try {
     const res = await axios.post("https://candidates-exam.herokuapp.com/api/v1/usuarios/",data)
     if (res.status==201) {
       console.log(res)
       cleanData()
     
     }else if(res.status=422){
           Swal.fire({
  title: 'Error!',
  text: 'ingre otro usuario y correo',
  icon: 'error',
  confirmButtonText: 'existe un usario con esos datos'
})
     }
     else{
       Swal.fire({
  title: 'Error!',
  text: 'Fuera de Servicio',
  icon: 'error',
  confirmButtonText: 'intenta mas tarde'
})
     return response
   } }catch (error) {
     return "error"
   }
  
     
    }
function registerUser(e){


   e.preventDefault()

   if (password.value==password_confirmation.value) {
     
     const user={
      nombre:nombre.value,
      email:email.value,
      password:password.value,
      password_confirmation:password_confirmation.value
      }
     apiRegister(user)
       router.replace({
         path:'/'
       })
     

    }else{
  Swal.fire({
  title: 'Error!',
  text: 'La contraseña no cociden',
  icon: 'error',
  confirmButtonText: 'intentar de nuevo'
})
    }
  }
function cleanData(){
     nombre.value =''
     email.value =''
     password.value =''
     password_confirmation.value =''
 }
onUpdated(()=>{
 

})


</script>

<template>
    <form class="row needs-validation" >
    <div class="row">
        <h1 >Register</h1>
    </div>
    <div class="row">

  <div class="row-auto">
      <label for="inputNombre"  class="form-label">Nombre</label>
    <input type="text" v-model="nombre" class="form-control" id="inputNombre" placeholder="Example Gt" required>
  </div> 
  <div class="row-auto">
      <label for="inputEmail" class="form-label">email</label>
    <input type="email" v-model="email" class="form-control" id="inputEmail" placeholder="examplegt@gmail.com" required>
  </div>      
  <div class="row-auto">
      <label for="inputPassword" class="form-label">Password</label>
    <input type="password" v-model="password" class="form-control" id="inputPassword" placeholder="Password" required>
  </div>
    <div class="row-auto">
        <label for="inputPassword_confirmation" class="form-label">Password Confirmation</label>
        <input  v-model="password_confirmation" type="password" class="form-control" id="inputPasswordConfirmation" placeholder="Password Confirmation" required>
    </div>
  <div class="col-auto">
      <button type="submit" @click="registerUser" class="btn btn-primary mb-3">R e g i s t e r</button>
  </div>
      </div>
  </form>
</template>