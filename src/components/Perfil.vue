<script setup>
import {onUpdated, ref, watch} from 'vue'

import axios from "axios"

import router from '../router';
import CargarCvModal from './modals/CargarCvModal.vue';


const urlPdf=ref("")
 const url=ref('')
const  usuario=ref('');
const showModal =ref(false);


 async function apiGetCurriculum(){
 try {
     const token = localStorage.getItem('token')
    const headers={
        "Authorization":`Bearer ${token}`,
        'Content-Type': 'multipart/form-data'

    }

     const res = await axios.get("https://candidates-exam.herokuapp.com/api/v1/usuarios/mostrar_cv",{headers})
     urlPdf.value= res.data.url
     console.log(res)
} catch (error) {
   Swal.fire({
            position: 'top-end',
            icon: 'error',
            title: 'error al cargar el archivo',
            showConfirmButton: false,
            timer: 1500
        })
 }
 }

function getCurriculum(){
apiGetCurriculum()

}


 (async()=>{
     const token = localStorage.getItem('token')
    const headers={
        "Authorization":`Bearer ${token}`,
        "Accept":'application/json'
    }

    try {
        const res=await axios.get("https://candidates-exam.herokuapp.com/api/v1/usuarios/",{headers})
        url.value=res.data.url

        usuario.value=res.data.usuario

    } catch (error) {
        console.log(error)
        localStorage.setItem('auth',false)
        router.replace({
            "path":'/'
        })
    }
})();



</script>
<template>
<div class="row ">
    <div class="col-auto">

        <p 

    class="urll">{{url}}</p>
    </div>
    <div class="col-auto">
        <button 
        @click="showModal=true"
        class="btn btn-primary">Cargar CV</button>
    </div>
    <div class="col">
        <button  class="btn btn-info"
        data-bs-toggle="modal" data-bs-target="#exampleModal"
        @click="getCurriculum"
        >Ver CV</button>
    </div>
    

</div>
    <Teleport to="body">
       <CargarCvModal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>Subir CV</h3>
      </template>
       </CargarCvModal>
    </Teleport>

<div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
  <div class="modal-dialog">
    <div class="modal-content">
      <div class="modal-header">
        <h5 class="modal-title" id="exampleModalLabel" >curriculum de {{url}}</h5>
        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
      </div>
      <div class="modal-body">
        
        <iframe :src="urlPdf" frameborder="0"/>
                       
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
      </div>
    </div>
  </div>
</div>

</template>
<style>
p .urll{
    color: black;
}

</style>