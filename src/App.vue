<script setup>
import { reactive, ref } from "vue";
import { uid } from "uid";
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import Paciente from "./components/Paciente.vue";

const pacientes = ref([]);

const btnAccion = ref(true)

const paciente = reactive({
  id: null,
  nombre: "",
  propietario: "",
  email: "",
  alta: "",
  sintomas: "",
});

const guardarPaciente = () => {
  if(paciente.id) {
    const { id } = paciente
    const idx = pacientes.value.findIndex((state) => state.id === id)
    pacientes.value[idx] = { ...paciente }
  } else {
    pacientes.value.push({
      ...paciente,
      id: uid()
    });
  }

  // Reiniciar el objeto
  Object.assign(paciente, {
    nombre: "",
    propietario: "",
    email: "",
    alta: "",
    sintomas: "",
    id: null
  });

  btnAccion.value = true
};

const editarPaciente = (id) => {
  btnAccion.value = false
  const pacienteEditar = pacientes.value.filter(paciente => paciente.id === id)[0]
  Object.assign(paciente, pacienteEditar)

}

const eliminarPaciente = (id) => {
  const nuevaLista = pacientes.value.filter(paciente => paciente.id !== id)
  console.log('eliminando', nuevaLista);
  pacientes.value = nuevaLista 
};

</script>

<template>
  <div class="container mx-auto mt-10 lg:mt-20">
    <Header />
    <div class="mt-10 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
        @eliminar-paciente="eliminarPaciente"
        :btnAccion="btnAccion"
      />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-medium text-3xl text-center">
          Administra tus pacientes
        </h3>
        <div v-if="pacientes.length > 0">
          <p class="text-lg mt-5 text-center mb-10">
            Información de
            <span class="text-indigo-600 font-bold">Pacientes</span>
          </p>
          <Paciente 
          v-for="paciente in pacientes" 
          :paciente="paciente" 
          @editar-paciente="editarPaciente"
          @eliminar-paciente="eliminarPaciente"
          />
        </div>
        <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
