<script setup>
import Header from "./components/Header.vue";
import Formulario from "./components/Formulario.vue";
import { ref } from "vue";

const pacientes = ref([]);
</script>

<template>
  <div class="container mx-auto mt-10 lg:mt-20">
    <Header />
    <div class="mt-10 md:flex">
      <Formulario />
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-medium text-3xl text-center">
          Administra tus pacientes
        </h3>
        <div v-if="pacientes.length > 0"></div>
        <p v-else class="mt-20 text-2xl text-center">No hay pacientes</p>
      </div>
    </div>
  </div>
</template>
