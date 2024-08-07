<script setup>
  import { ref } from 'vue';

  const nome = ref('Kitty');
  const estado = ref('inativo');

  const mudaEstado = () => {
    if (estado.value === 'inativo') {
      estado.value = 'pendente';
    } else if (estado.value === 'pendente') {
      estado.value = 'ativo';
    } else {
      estado.value = 'inativo';
    }
  };
</script>

<template>
  <h1>Olaaarrrr, {{ nome }}</h1>
  <p>O estado do usuário é {{ estado }}</p>
  <button @click="mudaEstado">Muda Estado</button>
  <br />
  <p v-if="estado === 'ativo'">Você pode fazer o que quiser!!!</p>
  <p v-else-if="estado === 'pendente'">Aguarde mais um pouco...</p>
  <p v-else>Você não tem permissão...</p>
</template>
