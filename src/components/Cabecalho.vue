<script setup>
const props = defineProps(['FiltroTarefa', 'TrocarFiltro'])
</script>
<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>você possui {{ props.FiltroTarefa}} tarefas {{ props.TrocarFiltro }}  </p>
    </header>
</template>