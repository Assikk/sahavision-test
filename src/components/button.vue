<template>
  <button class="py-2.5 px-3.5 rounded-md"
  :disabled="disabled">
    <slot></slot>
  </button>
</template>
<script setup lang="ts">
  defineOptions({
    name: 'ButtonComponent'
  })
  withDefaults(defineProps<{
    disabled?: boolean
  }>(), {
    disabled: false
  })
</script>
<style scoped>
  button:disabled {
    background: #789CAB;
    color: #FFFFFF80;
    cursor: not-allowed;
  }
  button {
    background: #038DB7;
    border: none;
    color: white;
  }
  button:not(:disabled):hover {
    background: #0A7194;
  }
</style>