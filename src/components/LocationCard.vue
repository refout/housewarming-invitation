<template>
  <div class="location-card">
    <div class="location-header">
      <span class="location-icon">{{ icon }}</span>
      <h3>{{ title }}</h3>
    </div>
    <div class="location-address">
      <p>{{ address }}</p>
    </div>
    <div class="navigation-buttons">
      <button @click="openGaodeMap" class="nav-btn gaode">
        <span class="btn-icon">🗺️</span>
        高德地图
      </button>
      <button @click="openBaiduMap" class="nav-btn baidu">
        <span class="btn-icon">📍</span>
        百度地图
      </button>
      <button @click="openTencentMap" class="nav-btn tencent">
        <span class="btn-icon">🗺️</span>
        腾讯地图
      </button>
    </div>
    <div class="copy-address">
      <button @click="copyAddress" class="copy-btn">
        <span class="btn-icon">📋</span>
        复制地址
      </button>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue'

const props = defineProps({
  title: {
    type: String,
    required: true
  },
  address: {
    type: String,
    required: true
  },
  icon: {
    type: String,
    default: '📍'
  },
  latitude: {
    type: Number,
    required: true
  },
  longitude: {
    type: Number,
    required: true
  }
})

// 打开高德地图
const openGaodeMap = () => {
  // 高德地图Web端导航URL
  const url = `https://uri.amap.com/marker?position=${props.longitude},${props.latitude}&name=${encodeURIComponent(props.title)}&coordinate=gaode`
  window.open(url, '_blank')
}

// 打开百度地图
const openBaiduMap = () => {
  // 百度地图Web端导航URL
  const url = `https://api.map.baidu.com/marker?location=${props.latitude},${props.longitude}&title=${encodeURIComponent(props.title)}&content=${encodeURIComponent(props.address)}&output=html`
  window.open(url, '_blank')
}

// 打开腾讯地图
const openTencentMap = () => {
  // 腾讯地图Web端导航URL
  const url = `https://apis.map.qq.com/uri/v1/marker?marker=coord:${props.latitude},${props.longitude};title:${encodeURIComponent(props.title)};addr:${encodeURIComponent(props.address)}`
  window.open(url, '_blank')
}

// 复制地址
const copyAddress = async () => {
  try {
    await navigator.clipboard.writeText(props.address)
    alert('地址已复制到剪贴板！')
  } catch (err) {
    // 降级方案：使用传统复制方法
    const textArea = document.createElement('textarea')
    textArea.value = props.address
    textArea.style.position = 'fixed'
    textArea.style.left = '-9999px'
    document.body.appendChild(textArea)
    textArea.select()
    try {
      document.execCommand('copy')
      alert('地址已复制到剪贴板！')
    } catch (err) {
      alert('复制失败，请手动复制地址')
    }
    document.body.removeChild(textArea)
  }
}
</script>

<style scoped>
.location-card {
  background: white;
  border-radius: 12px;
  padding: 20px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.location-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 20px rgba(0, 0, 0, 0.15);
}

.location-header {
  display: flex;
  align-items: center;
  margin-bottom: 15px;
}

.location-icon {
  font-size: 32px;
  margin-right: 10px;
}

.location-header h3 {
  font-size: 20px;
  color: #2c3e50;
  margin: 0;
}

.location-address {
  padding: 15px;
  background: #f8f9fa;
  border-radius: 8px;
  margin-bottom: 15px;
}

.location-address p {
  font-size: 15px;
  color: #555;
  margin: 0;
  line-height: 1.6;
}

.navigation-buttons {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
  margin-bottom: 15px;
}

.nav-btn {
  padding: 10px 15px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 5px;
}

.btn-icon {
  font-size: 16px;
}

.gaode {
  background: linear-gradient(135deg, #00C853 0%, #00E676 100%);
  color: white;
}

.gaode:hover {
  background: linear-gradient(135deg, #00E676 0%, #00C853 100%);
  transform: scale(1.05);
}

.baidu {
  background: linear-gradient(135deg, #2196F3 0%, #03A9F4 100%);
  color: white;
}

.baidu:hover {
  background: linear-gradient(135deg, #03A9F4 0%, #2196F3 100%);
  transform: scale(1.05);
}

.tencent {
  background: linear-gradient(135deg, #FF9800 0%, #FFC107 100%);
  color: white;
}

.tencent:hover {
  background: linear-gradient(135deg, #FFC107 0%, #FF9800 100%);
  transform: scale(1.05);
}

.copy-address {
  margin-top: 10px;
}

.copy-btn {
  width: 100%;
  padding: 10px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  color: white;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 14px;
  font-weight: 500;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 5px;
}

.copy-btn:hover {
  background: linear-gradient(135deg, #764ba2 0%, #667eea 100%);
  transform: scale(1.02);
}

@media (max-width: 600px) {
  .navigation-buttons {
    grid-template-columns: 1fr;
  }

  .nav-btn {
    padding: 12px;
  }
}
</style>
