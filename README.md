# 锅炉参数监控系统

这是一个基于Vue 3和Vite的锅炉参数监控系统前端应用。该应用允许用户输入锅炉相关参数，并根据选择的负荷比例显示相应的温度云图和温度折线图。

## 功能特点

- 输入8个锅炉参数
- 选择负荷比例(100%, 75%, 50%, 25%)
- 根据负荷比例显示对应的温度云图和温度折线图
- 响应式设计，适配不同屏幕尺寸

## 项目结构

\`\`\`
boiler-monitoring-system/
├── public/                 # 静态资源
│   └── favicon.svg         # 网站图标
├── src/                    # 源代码
│   ├── assets/             # 资源文件
│   │   ├── css/            # CSS样式
│   │   │   └── main.css    # 主样式文件
│   │   └── images/         # 图片资源
│   │       ├── cloud_*.png # 温度云图
│   │       └── line_*.png  # 温度折线图
│   ├── components/         # Vue组件
│   │   ├── ParameterInput.vue    # 参数输入组件
│   │   ├── LoadRatioSelector.vue # 负荷比例选择器组件
│   │   └── VisualizationCard.vue # 可视化卡片组件
│   ├── App.vue             # 主应用组件
│   └── main.js             # 应用入口
├── index.html              # HTML模板
├── package.json            # 项目依赖
├── vite.config.js          # Vite配置
└── README.md               # 项目说明
\`\`\`

## 安装与运行

1. 克隆项目
\`\`\`bash
git clone <repository-url>
cd boiler-monitoring-system
\`\`\`

2. 安装依赖
\`\`\`bash
npm install
\`\`\`

3. 开发模式运行
\`\`\`bash
npm run dev
\`\`\`

4. 构建生产版本
\`\`\`bash
npm run build
\`\`\`

5. 预览生产版本
\`\`\`bash
npm run preview
\`\`\`

## 自定义配置

如需自定义配置，请参考 [Vite配置参考](https://vitejs.dev/config/).
