<template>
  <div class="visualization-card">
    <h3>{{ title }}</h3>
    <div class="image-container">
      <img 
        :src="imageSrc" 
        :alt="title" 
        class="visualization-image"
        :style="{ transform: `scale(${zoomLevel})` }"
      >
      <div class="zoom-controls">
        <button @click="zoomIn" class="zoom-btn">+</button>
        <button @click="zoomOut" class="zoom-btn">-</button>
        <button @click="resetZoom" class="zoom-btn">重置</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  imageSrc: {
    type: String,
    required: true
  }
});

const zoomLevel = ref(1);
const ZOOM_STEP = 0.1;
const MAX_ZOOM = 2;
const MIN_ZOOM = 0.5;

const zoomIn = () => {
  if (zoomLevel.value < MAX_ZOOM) {
    zoomLevel.value += ZOOM_STEP;
  }
};

const zoomOut = () => {
  if (zoomLevel.value > MIN_ZOOM) {
    zoomLevel.value -= ZOOM_STEP;
  }
};

const resetZoom = () => {
  zoomLevel.value = 1;
};
</script>

<style scoped>
.visualization-card {
  border: 1px solid var(--border-color);
  border-radius: 8px;
  overflow: hidden;
}

.visualization-card h3 {
  padding: 15px;
  background-color: var(--background-color);
  margin: 0;
  text-align: center;
  color: var(--secondary-color);
}

.image-container {
  padding: 15px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
  min-height: 300px;
}

.zoom-controls {
  display: flex;
  gap: 8px;
  background-color: var(--card-background);
  padding: 8px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.zoom-btn {
  width: 32px;
  height: 32px;
  border: 1px solid var(--border-color);
  background-color: white;
  border-radius: 4px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 16px;
  transition: all 0.3s;
}

.zoom-btn:hover {
  background-color: var(--hover-color);
  border-color: var(--primary-color);
}

.visualization-image {
  max-width: 100%;
  max-height: 400px;
  object-fit: contain;
  transition: transform 0.3s ease;
  transform-origin: center center;
}
</style>
