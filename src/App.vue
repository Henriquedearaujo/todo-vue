<script setup>
import { reactive } from 'vue';

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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>você possui {{ getTarefasFIltradas().length }} tarefas {{ estado.filtro }}</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required
            type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="">Todas as tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefas in getTarefasFIltradas()">
        <input @change="evento => tarefas.finalizada = evento.target.checked" :checked="tarefas.finalizada"
          :id="tarefas.titulo" type="checkbox">
        <label :class="{ done: tarefas.finalizada }" class="ms-3" :for="tarefas.titulo">
          {{ tarefas.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
