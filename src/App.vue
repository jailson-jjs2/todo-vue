<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      {
       titulo: 'Estudar ES6',
       finalizada: false,
      },
      {
       titulo: 'Estudar SASS',
       finalizada: false,
      },
      {
       titulo: 'Malhar na academia',
       finalizada: true,
      },
    ]
  })

  /* FUNÇAÕ PARA PEGAR TAREFAS */
  const getTarefasPendentes = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada) 
  }
  const getTarefasFinalizadas = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada) 
  }

  const getTarefasFiltradas = () => {
    const filtro = estado.filtro; /* TB PODE USAR: {filtro} = estado */

    if (filtro === 'pendentes') {
      return getTarefasPendentes();
    } else if (filtro === 'finalizadas') {
      return getTarefasFinalizadas();
    } else {
      return estado.tarefas;
    }
  };

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaTemp,
      finalizada: false,
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
  }

</script>

<!-- HTML -->
<template>

  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      Você possui {{ getTarefasPendentes().length }} tarefas pendentes
    </header>
    <form @submit.prevent="cadastraTarefa"><!-- prevent PARA Ñ ATUALIZAR A PAG NO CAD -->
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required class="form-control" type="text" placeholder="Informe a descrião da tarefa">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()"><!--v-for PEGA ARRAY -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo"><!--PEGANDO INFORMAÇOES DA tarefa E DO CSS .done  -->
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>

<!-- CSS -->
<style scoped>

  .done {
    text-decoration: line-through;
  }

</style>
