<script setup>
import { computed, reactive, ref } from 'vue';
import Alerta from './Alerta.vue';
import paciente from '../App.vue';

const alerta = reactive({
    tipo:'',
    mensaje:''
})

const emit = defineEmits(['update:nombre','update:propietario','update:email','update:alta','update:sintomas','guardar-paciente']);
const props = defineProps({
    nombre:{type:[String,null],required:true},
    propietario:{type:String,required:true},
    email:{type:String,required:true},
    alta:{type:String,required:true},
    sintomas:{type:String,required:true},
})

const validar = () => {
   if(Object.values(props).includes('')){
        alerta.mensaje = 'Todos los campos son obligatorios';
        alerta.tipo = 'error'
        return
    }
    else {

            alerta.mensaje = 'Todos los campos bien rellenados'
            alerta.tipo = 'exito'
            emit('guardar-paciente')
            setTimeout(() => {
                 alerta.mensaje = '';
                 alerta.tipo = ''
            }, 2000);
            return
        }
}


const editando = computed(() => {
    return props.id 

})


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
    :value="nombre"
    @input="$emit('update:nombre',$event.target.value)"
    > 
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
    :value="propietario"
    @input="$emit('update:propietario',$event.target.value)"
    > 
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
    :value="email"
    @input="$emit('update:email',$event.target.value)"
    > 

</div>
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold" for="fecha">
        fecha de alta
    </label>
    <input 
    type="date" 
    id="fecha"  
    class="border-2 px-4 w-full mt-2 placeholder-gray-200 rounded-md"
    :value="alta"
    @input="$emit('update:alta',$event.target.value)"
    > 

</div>
<div class="mb-5">
    <label class="block text-gray-700 uppercase font-bold " for="sintomas">
       Sintomas Paciente
    </label>
    <textarea 
    id="sintomas" 
    placeholder="Describe los sintomas del paciente"  
    :value="sintomas"
    class="h-40 px-2 border w-full mt-2 placeholder-gray-800 rounded-md" @input="$emit('update:sintomas',$event.target.value)"
    > </textarea>


</div>

<input type="submit"
       class="bg-indigo-600 w-full p-3 text-white uppercase font-bold hover:bg-indigo-900 transition-colors cursor-pointer " :value="[editando ? 'Guardar cambio' : 'Guardado el paciente']"
>
            </form>
    </div>
</template>

