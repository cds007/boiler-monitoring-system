<template>
  <div class="container">
    <header class="header">
      <h1>锅炉参数监控系统</h1>
      <div class="load-display">
        <div class="load-label">Load (MW)</div>
        <div class="load-value">1000</div>
      </div>
    </header>

    <div class="parameters-section">
      <h2>输入参数</h2>
      <div class="parameters-grid">
        <ParameterInput
          label="实际耗煤量 (t/h)"
          id="coal"
          v-model="parameters.coal"
        />
        <ParameterInput
          label="一次风量 (kg/s)"
          id="primaryAir"
          v-model="parameters.primaryAir"
        />
        <ParameterInput
          label="二次风量 (kg/s)"
          id="secondaryAir"
          v-model="parameters.secondaryAir"
        />
        <ParameterInput
          label="燃尽风量 (kg/s)"
          id="burnoutAir"
          v-model="parameters.burnoutAir"
        />
        <ParameterInput
          label="一次风风速 (m/s)"
          id="secondaryAirSpeed"
          v-model="parameters.secondaryAirSpeed"
        />
        <ParameterInput
          label="内二次风风速 (m/s)"
          id="innerSecondaryAirSpeed"
          v-model="parameters.innerSecondaryAirSpeed"
        />
        <ParameterInput
          label="外二次风风速 (m/s)"
          id="outerSecondaryAirSpeed"
          v-model="parameters.outerSecondaryAirSpeed"
        />
        <ParameterInput
          label="燃尽风风速 (m/s)"
          id="burnoutAirSpeed"
          v-model="parameters.burnoutAirSpeed"
        />
      </div>

      <LoadRatioSelector
        v-model="selectedLoadRatio"
        :options="loadRatios"
        @update:modelValue="handleLoadRatioChange"
      />
    </div>

    <div class="visualization-section">
      <h2>温度可视化</h2>
      <div class="visualization-container">
        <VisualizationCard
          title="温度云图"
          :imageSrc="getCloudImagePath()"
        />
        <VisualizationCard
          title="温度折线图"
          :imageSrc="getLineImagePath()"
        />
      </div>
    </div>

    <LoadingSpinner :show="isLoading" />
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';
import ParameterInput from './components/ParameterInput.vue';
import LoadRatioSelector from './components/LoadRatioSelector.vue';
import VisualizationCard from './components/VisualizationCard.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';

// 参数初始化
const parameters = reactive({
  coal: 0,
  primaryAir: 0,
  secondaryAir: 0,
  burnoutAir: 0,
  secondaryAirSpeed: 0,
  innerSecondaryAirSpeed: 0,
  outerSecondaryAirSpeed: 0,
  burnoutAirSpeed: 0
});

// 负荷比例选项
const loadRatios = [100, 75, 50, 25];
const selectedLoadRatio = ref(100);
const isLoading = ref(false);

// 在script部分导入图片
import cloud100 from './assets/images/cloud_100.png';
import cloud75 from './assets/images/cloud_75.png';
import cloud50 from './assets/images/cloud_50.png';
import cloud25 from './assets/images/cloud_25.png';
import line100 from './assets/images/line_100.png';
import line75 from './assets/images/line_75.png';
import line50 from './assets/images/line_50.png';
import line25 from './assets/images/line_25.png';

// 处理负荷比例变化
const handleLoadRatioChange = async (newRatio) => {
  isLoading.value = true;
  // 模拟2秒的加载时间
  await new Promise(resolve => setTimeout(resolve, 2000));
  isLoading.value = false;
};

// 获取云图路径
const getCloudImagePath = () => {
  switch (selectedLoadRatio.value) {
    case 100: return cloud100;
    case 75: return cloud75;
    case 50: return cloud50;
    case 25: return cloud25;
    default: return cloud100;
  }
};

// 获取折线图路径
const getLineImagePath = () => {
  switch (selectedLoadRatio.value) {
    case 100: return line100;
    case 75: return line75;
    case 50: return line50;
    case 25: return line25;
    default: return line100;
  }
};
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 30px;
  padding-bottom: 15px;
  border-bottom: 1px solid var(--border-color);
}

h1, h2 {
  color: var(--secondary-color);
}

.load-display {
  background-color: var(--card-background);
  padding: 15px 25px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  text-align: center;
}

.load-label {
  font-size: 14px;
  color: var(--text-color);
  margin-bottom: 5px;
}

.load-value {
  font-size: 24px;
  font-weight: bold;
  color: var(--primary-color);
}

.parameters-section {
  background-color: var(--card-background);
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
  margin-bottom: 30px;
}

.parameters-section h2 {
  margin-bottom: 20px;
}

.parameters-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 20px;
}

.visualization-section {
  background-color: var(--card-background);
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.05);
}

.visualization-section h2 {
  margin-bottom: 20px;
}

.visualization-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(400px, 1fr));
  gap: 20px;
}

@media (max-width: 768px) {
  .parameters-grid {
    grid-template-columns: 1fr;
  }

  .visualization-container {
    grid-template-columns: 1fr;
  }

  .header {
    flex-direction: column;
    gap: 15px;
  }
}
</style>
