<script setup>
  const props = defineProps(['tarefas'])
</script>

<template>
  <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in props.tarefas"><!--v-for PEGA ARRAY -->
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
        <label :class="{done: tarefa.finalizada}" class="ms-3" :for="tarefa.titulo"><!--PEGANDO INFORMAÇOES DA tarefa E DO CSS .done  -->
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
</template>

<style scoped>

  .done {
    text-decoration: line-through;
  }

</style>