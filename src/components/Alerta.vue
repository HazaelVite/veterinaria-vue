<script setup>
const props = defineProps({
    alerta: {
        type: Object,
        required: true
    }
})
</script>


<template>
    <div 
    class="text-white text-center uppercase font-bold bg-red-500 rounded-md p-3 mb-3"
    >
        {{ alerta.mensaje }}
    </div>
</template>