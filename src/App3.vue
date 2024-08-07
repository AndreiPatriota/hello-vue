<script setup>
  import { ref } from 'vue';
  import TaskCard from './components/TaskCard.vue';

  let fakeCont = 0;
  const tarefas = ref([]);
  const campoTitulo = ref('');
  const campoDescricao = ref('');
  const campoPrazo = ref(Date.now());

  const adicionaTarefa = (texto) => {
    tarefas.value.push({
      id: fakeCont,
      titulo: campoTitulo.value,
      descricao: campoDescricao.value,
      prazo: campoPrazo.value,
      completa: false,
    });

    fakeCont += 1;
    campoTitulo.value = '';
    campoDescricao.value = '';
  };

  const deletaTarefa = (id) => {
    tarefas.value.splice(id, 1);
  };
</script>

<template>
  <h1>Lista de Afazeres:</h1>
  <form @submit.prevent="adicionaTarefa">
    <div>
      <label for="iTitulo"></label>
      <input type="text" id="iTitulo" v-model="campoTitulo" />
    </div>
    <div>
      <label for="iDescricao"></label>
      <input type="text" id="iDescricao" v-model="campoDescricao" />
    </div>
    <div>
      <label for="iPrazo"></label>
      <input type="date" id="iPrazo" v-model="campoPrazo" />
    </div>
    <button type="submit">Adiciona</button>
  </form>
  <br />
  <ul>
    <li v-for="(tarefa, index) in tarefas" :key="tarefa.id">
      <TaskCard
        :titulo="tarefa.titulo"
        :descricao="tarefa.descricao"
        :prazo="tarefa.prazo" />
    </li>
  </ul>
</template>
