<script setup>
import { reactive, ref } from 'vue';
import Alerta from './Alerta.vue';


const alerta = reactive({
    tipo:'',
    mensaje:'',
})






const paciente = reactive({
    nombre:'',
    propietario:'',
    email:'',
    fecha:'',
    sintomas:'',
})
const validar = () => {
   if(Object.values(paciente).includes('')){
        alerta.mensaje = 'Todos los campos son obligatorios';
        alerta.tipo = 'error'
        return
    }
    else {
            alerta.mensaje = 'Todos los campos bien rellenados'
            alerta.tipo = 'exito'
            return
        }
}



</script>
<template>
   
    <div class="md:w-1/2">
            <h2 class="font-black text-3xl text-center">Seguimiento pacientes</h2>
            <p class="text-lg mt-5 text-center mb-10">
                <span>anade pacientes y
                    <span class="text-indigo-600 font-bold">administralos</span>
                </span>
            </p>
            <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
            
            />
<form action="" v-on:submit.prevent="validar" class="bg-white  shadow-md rounded-lg py-10 px-5 mb-10">
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold" for="mascota">
        Nombre de Mascota
    </label>
    <input 
    type="text" 
    id="mascota" 
    placeholder="Nombre de la mascota" 
    class="border px-2 w-full mt-2 placeholder-gray-200 rounded-md"
    v-model="paciente.nombre"> 
</div>
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold" for="propietario">
        Nombre de propietario
    </label>
    <input 
    type="text" 
    id="propietario" 
    placeholder="Nombre de la mascota" 
    class="border px-2 w-full mt-2 placeholder-gray-200 rounded-md"
    v-model="paciente.propietario"> 
</div>
<!-- TODO:SEPARACION -->
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold" for="email">
        email
    </label>
    <input 
    type="email" 
    id="email" 
    placeholder="Nombre de la mascota" 
    class="border px-2 w-full mt-2 placeholder-gray-200 rounded-md"
    v-model="paciente.email"> 

</div>
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold" for="fecha">
        fecha de alta
    </label>
    <input 
    type="date" 
    id="fecha"  
    class="border-2 px-4 w-full mt-2 placeholder-gray-200 rounded-md"
    v-model="paciente.fecha"> 

</div>
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold " for="sintomas">
       Sintomas Paciente
    </label>
    <textarea 
    id="sintomas" 
    placeholder="Describe los sintomas del paciente"  
    class="h-40 px-2 border w-full mt-2 placeholder-gray-800 rounded-md" v-model="paciente.sintomas"> </textarea>


</div>

<input type="submit"
       class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-900 transition-colors cursor-pointer " value="registrar paciente"
>
            </form>
    </div>
</template>

