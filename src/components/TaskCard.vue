<script setup>
  const props = defineProps({
    titulo: {
      type: String,
      default: 'Título',
    },
    descricao: {
      type: String,
      default: 'Descrição',
    },
    prazo: {
      type: Date,
      default: Date.now(),
    },
    completa: {
      type: Boolean,
      default: false,
    },
  });
</script>

<template>
  <article :class="{ completa: props.completa }">
    <header>
      <h2>{{ props.titulo }}</h2>
    </header>
    <span
      ><input type="checkbox" :checked="props.completa" />
      {{ props.descricao }}</span
    >
    <footer>
      <small>Prazo: {{ props.prazo }}</small>
    </footer>
  </article>
</template>

<style>
  article {
    width: 400px;
    height: 100px;
    background-color: pink;
    border-style: solid;
    border-radius: 5px;
    padding: 20px;
  }
  .completa {
    background-color: brown;
  }
</style>
