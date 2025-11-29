<template>
  <input
    :value="modelValue"
    @input="e => $emit('update:modelValue', (e.target as HTMLInputElement).value)"
    type="text"
    class="ui-input"
    :class="{ invalid: error }"
    :placeholder="placeholder"
  />
</template>

<script setup lang="ts">
defineProps<{
  modelValue: string
  error?: boolean
  placeholder?: string
}>()
defineEmits<{
  (e: 'update:modelValue', v: string): void
}>()
</script>

<style scoped>
.ui-input {
  height: 36px;
  padding: 0 10px;
  border: 1px solid var(--color-Disabled);
  border-radius: 4px;
  font-size: 14px;
  flex: 1;
}
.invalid {
border-color: var(--color-error);
}
</style>
