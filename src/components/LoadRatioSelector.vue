<template>
  <div class="load-ratio-section">
    <h3>{{ title }}</h3>
    <div class="load-ratio-options">
      <button 
        v-for="ratio in options" 
        :key="ratio" 
        :class="['load-ratio-btn', { active: modelValue === ratio }]"
        @click="$emit('update:modelValue', ratio)"
      >
        {{ ratio }}%
      </button>
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    default: '负荷比例 (%)'
  },
  options: {
    type: Array,
    default: () => [100, 75, 50, 25]
  },
  modelValue: {
    type: Number,
    required: true
  }
});

defineEmits(['update:modelValue']);
</script>

<style scoped>
.load-ratio-section {
  margin-top: 30px;
}

.load-ratio-section h3 {
  margin-bottom: 15px;
  color: var(--secondary-color);
}

.load-ratio-options {
  display: flex;
  gap: 15px;
  flex-wrap: wrap;
}

.load-ratio-btn {
  padding: 10px 20px;
  background-color: var(--card-background);
  border: 1px solid var(--border-color);
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 14px;
}

.load-ratio-btn:hover {
  background-color: var(--hover-color);
}

.load-ratio-btn.active {
  background-color: var(--primary-color);
  color: white;
  border-color: var(--primary-color);
}
</style>
