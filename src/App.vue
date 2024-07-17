<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';
const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'Estudar sasss',
      finalizada: false,
    },
    {
      titulo: 'Ir para academia',
      finalizada: true,
    }
  ]
})

//funçoes para Filtrar itens
const getTarefaPendentes = () => {
  return estado.tarefas.filter(tarefas => !tarefas.finalizada)
}

const getTarefaFinalizadas = () => {
  return estado.tarefas.filter(tarefas => tarefas.finalizada)
}

const getTarefasFIltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefaPendentes();
    case 'finalizadas':
      return getTarefaFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <Cabecalho :-trocar-filtro="estado.filtro" :-filtro-tarefa="getTarefasFIltradas().length"/>
    <Formulario :-trocar-filtro="evento => estado.filtro = evento.target.value" 
      :tarefa-temp="estado.tarefaTemp" 
      :edita-tarefa-temp="evento => estado.tarefaTemp = evento.target.value" 
      :cadastra-tarefas="cadastraTarefa" />
      <ListaDeTarefas :tarefas="getTarefasFIltradas()" />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
