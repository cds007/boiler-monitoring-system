<template>
  <div class="parameter-item">
    <label :for="id">{{ label }}</label>
    <input 
      type="number" 
      :id="id" 
      :value="modelValue"
      @input="updateValue"
      step="0.1" 
      min="0"
    >
  </div>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  label: {
    type: String,
    required: true
  },
  id: {
    type: String,
    required: true
  },
  modelValue: {
    type: Number,
    required: true
  }
});

const emit = defineEmits(['update:modelValue']);

const updateValue = (event) => {
  const value = parseFloat(event.target.value);
  emit('update:modelValue', value);
};
</script>

<style scoped>
.parameter-item {
  display: flex;
  flex-direction: column;
}

.parameter-item label {
  margin-bottom: 8px;
  font-size: 14px;
}

.parameter-item input {
  padding: 10px;
  border: 1px solid var(--border-color);
  border-radius: 4px;
  font-size: 14px;
  transition: border-color 0.3s;
}

.parameter-item input:focus {
  outline: none;
  border-color: var(--primary-color);
}
</style>
