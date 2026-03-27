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
        高德地图导航
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
  background: rgba(255, 255, 255, 0.95);
  border-radius: 16px;
  padding: 25px;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.15);
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  backdrop-filter: blur(10px);
}

/* 桌面端优化 */
@media (min-width: 769px) {
  .location-card {
    padding: 30px;
    border-radius: 18px;
  }

  .location-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 12px 40px rgba(0, 0, 0, 0.2);
  }

  .location-icon {
    font-size: 40px;
    margin-right: 15px;
  }

  .location-header h3 {
    font-size: 24px;
  }

  .location-address {
    padding: 20px;
    border-radius: 12px;
    margin-bottom: 20px;
  }

  .location-address p {
    font-size: 17px;
  }

  .navigation-buttons {
    margin-bottom: 20px;
  }

  .nav-btn {
    padding: 16px 24px;
    font-size: 17px;
    border-radius: 12px;
  }

  .btn-icon {
    font-size: 22px;
  }

  .copy-btn {
    padding: 14px;
    font-size: 16px;
    border-radius: 12px;
  }
}

/* 大屏幕优化 */
@media (min-width: 1200px) {
  .location-card {
    padding: 35px;
  }

  .location-icon {
    font-size: 45px;
  }

  .location-header h3 {
    font-size: 26px;
  }

  .location-address {
    padding: 22px;
  }

  .location-address p {
    font-size: 18px;
  }

  .nav-btn {
    padding: 18px 26px;
    font-size: 18px;
  }

  .copy-btn {
    padding: 16px;
    font-size: 17px;
  }
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
  margin-bottom: 15px;
}

.nav-btn {
  width: 100%;
  padding: 12px 15px;
  border: none;
  border-radius: 8px;
  cursor: pointer;
  font-size: 15px;
  font-weight: 500;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
}

.btn-icon {
  font-size: 18px;
}

.gaode {
  background: linear-gradient(135deg, #00C853 0%, #00E676 100%);
  color: white;
}

.gaode:hover {
  background: linear-gradient(135deg, #00E676 0%, #00C853 100%);
  transform: scale(1.02);
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
  .location-card {
    padding: 20px;
    border-radius: 14px;
  }

  .location-header {
    justify-content: center;
    margin-bottom: 15px;
  }

  .location-icon {
    font-size: 32px;
    margin-right: 10px;
  }

  .location-header h3 {
    font-size: 20px;
  }

  .location-address {
    padding: 15px;
    margin-bottom: 15px;
  }

  .location-address p {
    font-size: 15px;
    line-height: 1.6;
  }

  .navigation-buttons {
    margin-bottom: 15px;
  }

  .nav-btn {
    padding: 18px 12px;
    font-size: 17px;
    min-height: 56px;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
    -webkit-user-select: none;
  }

  .nav-btn:active {
    transform: scale(0.98);
    opacity: 0.9;
  }

  .btn-icon {
    font-size: 22px;
  }

  .copy-btn {
    padding: 16px;
    font-size: 16px;
    min-height: 52px;
    -webkit-tap-highlight-color: transparent;
    user-select: none;
    -webkit-user-select: none;
  }

  .copy-btn:active {
    transform: scale(0.98);
    opacity: 0.9;
  }

  .location-card:hover {
    transform: none;
  }

  .gaode:hover,
  .copy-btn:hover {
    transform: none;
  }
}

/* 超小屏幕优化 */
@media (max-width: 375px) {
  .location-card {
    padding: 12px;
  }

  .location-icon {
    font-size: 24px;
  }

  .location-header h3 {
    font-size: 16px;
  }

  .location-address p {
    font-size: 13px;
  }

  .nav-btn,
  .copy-btn {
    padding: 12px;
    font-size: 14px;
  }
}

/* 触摸设备优化 */
@media (hover: none) and (pointer: coarse) {
  .location-card:hover {
    transform: none;
    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  }

  .nav-btn:hover,
  .copy-btn:hover {
    transform: none;
  }
}
</style>
