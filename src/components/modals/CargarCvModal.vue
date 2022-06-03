<script setup>

import Swal from 'sweetalert2'
import axios from 'axios';


let insFormData=null;
const props = defineProps({
  show: Boolean
})

async function loadpdf (data){
try {

    const res =await axios.post(`https://candidates-exam.herokuapp.com/api/v1/usuarios/${localStorage.getItem("url")}/cargar_cv`,data,{
        headers: {
            "Authorization":`Bearer ${localStorage.getItem("token")}`,
            'Content-Type': 'multipart/form-data'
            }
            })
            console.log(res)
    return       
} catch (error) {
    
}


}

function onFileChange(e){
    const size=e.target.files[0].size/1048576;
       if (size>5) {
        
            Swal.fire({
            position: 'top-end',
            icon: 'error',
            title: 'Solo DEbe cargar archivos pdf menor a 5mb',
            showConfirmButton: false,
            timer: 1500
        })

        e.target.value=""
        }else{

            insFormData=new FormData();

            insFormData.append("curriculum",e.target.files[0]);

        }

}

function uploadfile(){
if(insFormData){
            loadpdf(insFormData)

}
else{
      Swal.fire({
            position: 'top-start',
            icon: 'error',
            title: 'Dedes Cargar archivo pdf',
            showConfirmButton: false,
            timer: 1500
        })
}
}

</script>

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <slot name="header">Cargar CV</slot>
          </div>

          <div class="modal-body">
           <input 
           
           Accept=".pdf"
           @change="onFileChange"
           class="btn-primary form-control"
           type="file" label="Cargar cv">

          </div>

          <div class="modal-footer">
           
              <button
                class="modal-default-button btn btn-danger"
                @click="$emit('close')"
              >Cancelar</button>
             
              <button
                class="modal-default-button btn btn-primary"
                @click="uploadfile "
              >Aceptar</button>
            
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 400px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
}

.modal-header h3 {
  margin-top: 0;
  color: #4ea2c9;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

/*
 * The following styles are auto-applied to elements with
 * transition="modal" when their visibility is toggled
 * by Vue.js.
 *
 * You can easily play with the modal transition by editing
 * these styles.
 */

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}
</style>