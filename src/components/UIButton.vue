<template>
  <button
    type="submit"
    class="ui-button"
    :disabled="disabled"
  >
    <slot />
  </button>
</template>

<script setup lang="ts">
defineProps<{
  disabled?: boolean
}>()
</script>

<style scoped>
.ui-button {
  height: 36px;
  padding: 0 16px;
  border: none;
  border-radius: 4px;
  background: var(--color-blue);
  color: var(--color-white);
  font-size: 14px;
  cursor: pointer;
}
.ui-button:disabled {
  background: var(--color-Disabled);
  cursor: not-allowed;
}
</style>
