<template>
  <select
    :value="modelValue"
    @change="e => $emit('update:modelValue', (e.target as HTMLSelectElement).value)"
    class="ui-select"
  >
    <option v-for="opt in options" :key="opt" :value="opt">{{ opt }}</option>
  </select>
</template>

<script setup lang="ts">
defineProps<{
  modelValue: string
  options: string[]
}>()
defineEmits<{
  (e: 'update:modelValue', v: string): void
}>()
</script>

<style scoped>
.ui-select {
  height: 36px;
  padding: 0 8px;
  border: 1px solid var(--color-Disabled);
  border-radius: 4px;
  font-size: 14px;
  background: var(--color-white);
}
</style>
