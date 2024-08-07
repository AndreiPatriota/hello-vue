<script setup>
  const props = defineProps({
    bgColor: {
      type: String,
      default: 'gray',
    },
  });
</script>

<template>
  <div :class="`bg-${props.bgColor}-100 p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>
