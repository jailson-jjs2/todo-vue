<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import ListaDeTarefas from './components/ListaDeTarefas.vue'

  const estado = reactive({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
      
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

    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :trocarFiltro="evento => estado.filtro = evento.target.value" 
      :tarefaTemp="estado.tarefaTemp" 
      :editaTarefaTemp="evento => estado.tarefaTemp = evento.target.value" 
      :cadastraTarefa="cadastraTarefa" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
    
  </div>

</template>



