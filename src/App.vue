    <script setup>
    import Header from './components/Header.vue';
    import Formulario from './components/Formulario.vue';
    import { ref,reactive, onMounted, watch } from 'vue';
    import Paciente from './components/Paciente.vue'
    import {uid} from 'uid';

    const pacientes = ref([]);
    const paciente = reactive({
      id:null,
      nombre:'',
      propietario:'',
      email:'',
      fecha:'',
      sintomas:'',
    })
    const guardarPaciente = () => {
      if(paciente.id) {
        const {id} = paciente;
        const i = pacientes.value.findIndex((pacienteState) => {pacienteState.id === id})
        pacientes.value[i] = {...paciente}
      }
      pacientes.value.push({...paciente,id:uid()})
      paciente.nombre = '';
      paciente.propietario = '';
      paciente.email = '';
      paciente.alta = '';
      paciente.sintomas = '';
      paciente.id = null;
    }
    const actualizarPaciente = (id) => {
      const pacienteEditear = paciente.value.filter(paciente => paciente.id === id)[0]  
      Object.assign(paciente,pacienteEditear)
    }
    
    const eliminarPaciente = (id) => {
      pacientes.value = pacientes.value.filter(paciente => paciente.id !== id)
    }
    watch(pacientes,() => {
      guardarLocalStorage
    },{
      deep:true
    })
     
    const guardarLocalStorage = () => {
      localStorage.setItem('pacientes',JSON.stringify(pacientes.value))
    }
    onMounted(()=>{
      const pacientesStorage = localStorage.getItem('pacientes')
      if(pacientesStorage){
        pacientes.value = JSON.parse(pacientesStorage)
      }
    })
    </script>



<template>
  <div class="container mx-auto mt-20">
    <Header/>
    <div class="mt-12 md:flex">
      <Formulario
      v-model:nombre="paciente.nombre"
      v-model:propietario="paciente.propietario"
      v-model:email="paciente.email"
      v-model:alta="paciente.alta"
      v-model:sintomas="paciente.sintomas"
      @guardar-paciente="guardarPaciente"
      />
      <div class="w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center">Administra tus pacientes</h3>
        <div v-if="pacientes.length > 0">
        <p> class="text-lg mt-5 text-center mb-10">
                <span>Informacion de
                    <span class="text-indigo-600 font-bold">Pacientes</span>
                </span>
            </p>
          <Paciente 
          v-for="paciente in pacientes"
          :paciente="paciente"
          @actualizar-paciente="actualizarPaciente"
          @eliminar-paciente="eliminarPaciente"

          />



        </div>
        <p v-else class="mt-10 text-2xl text-center " > No hay pacientes</p>


      </div>

    </div>
  </div>
</template>


