<script setup>
import { reactive } from "vue";
import Alerta from "./Alerta.vue";

const alerta = reactive({
  tipo: "",
  mensaje: "",
});

const emit = defineEmits(['update:nombre', 'update:propietario', 'update:email', 'update:alta', 'update:sintomas', 'guardar-paciente', 'eliminar-paciente'])

const props = defineProps({
  nombre: {
    type: String,
    required: true
  },
  propietario: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true
  },
  alta: {
    type: String,
    required: true
  },
  sintomas: {
    type: String,
    required: true
  }
})

const handleSubmit = () => {
  if (Object.values(props).includes("")) {
    (alerta.tipo = "error"),
      (alerta.mensaje = "Todos los campos son obligatorios");
    return;
  }

  emit('guardar-paciente')
};
</script>

<template>
  <div class="md:w-1/2">
    <h2 class="text-3xl font-medium text-center">Seguimiento pacientes</h2>
    <p class="text-lg mt-5 mb-10 text-center">
      Añade pacientes y
      <span class="text-indigo-600 font-medium">Administralos</span>
    </p>
    <Alerta v-if="alerta.mensaje" :alerta="alerta" />
    <form
      class="bg-white shadow-md rounded-lg py-10 px-5 mb-10"
      @submit.prevent="handleSubmit"
    >
      <div class="mb-5">
        <label for="mascota" class="block text-gray-700 uppercase font-medium">
          Nombre mascota
        </label>
        <input
          id="mascota"
          type="text"
          placeholder="Nombre de la mascota"
          class="border-2 w-full p-2 mt-3 placeholder-gray-400"
          :value="nombre"
          @input="$emit('update:nombre', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label
          for="propietario"
          class="block text-gray-700 uppercase font-medium"
        >
          Nombre propietario
        </label>
        <input
          id="propietario"
          type="text"
          placeholder="Nombre del propietario"
          class="border-2 w-full p-2 mt-3 placeholder-gray-400"
          :value="propietario"
          @input="$emit('update:propietario', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="email" class="block text-gray-700 uppercase font-medium">
          Email
        </label>
        <input
          id="email"
          type="email"
          placeholder="Email del propietario"
          class="border-2 w-full p-2 mt-3 placeholder-gray-400"
          :value="email"
          @input="$emit('update:email', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="alta" class="block text-gray-700 uppercase font-medium">
          Alta
        </label>
        <input
          id="alta"
          type="date"
          placeholder="Fecha de alta"
          class="border-2 w-full p-2 mt-3 placeholder-gray-400"
          :value="email"
          @input="$emit('update:alta', $event.target.value)"
        />
      </div>

      <div class="mb-5">
        <label for="sintomas" class="block text-gray-700 uppercase font-medium">
          Sintomas
        </label>
        <textarea
          id="sintomas"
          placeholder="Escribe los sintomas del paciente"
          class="border-2 w-full p-2 mt-3 placeholder-gray-400 h-40"
          :value="sintomas"
          @input="$emit('update:sintomas', $event.target.value)"
        />
      </div>

      <input
        type="submit"
        class="bg-indigo-600 w-full p-3 text-white uppercase font-medium hover:bg-indigo-800 cursor-pointer transition-colors"
        value="Registrar paciente"
      />
    </form>
  </div>
</template>
