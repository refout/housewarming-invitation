<template>
  <div class="invitation-container">
    <!-- 第一张卡片：邀请标题 -->
    <section class="card-section">
      <div class="invitation-header">
        <div class="header-decoration">
          <span class="decoration-icon">🏠</span>
        </div>
        <h1 class="title">乔迁之喜</h1>
        <p class="subtitle">诚挚邀请您共襄盛举</p>
      </div>
      <div class="scroll-hint">
        <span class="hint-icon">👆</span>
        <span class="hint-text">向上滑动</span>
      </div>
    </section>

    <!-- 第二张卡片：邀请内容 -->
    <section class="card-section">
      <div class="invitation-content-card">
        <span class="card-icon">🎉</span>
        <h2>亲爱的亲朋好友</h2>
        <p class="message">
          良辰吉日，乔迁新居！<br />
          在这个喜庆的日子里，我们诚挚地邀请您来参加我们的乔迁宴会，<br />
          与我们共同分享这份喜悦！
        </p>
      </div>
    </section>

    <!-- 第三张卡片：活动时间 -->
    <section class="card-section">
      <div class="event-details">
        <div class="detail-item">
          <span class="detail-icon">📅</span>
          <div class="detail-content">
            <h3>活动时间</h3>
            <p>{{ eventDate }}</p>
          </div>
        </div>

        <div class="detail-item">
          <span class="detail-icon">🍽️</span>
          <div class="detail-content">
            <h3>活动流程</h3>
            <p>上午 10:00 - 新家参观</p>
            <p>中午 12:00 - 乔迁午宴</p>
          </div>
        </div>
      </div>
    </section>

    <!-- 第四张卡片：新家地址 -->
    <section class="card-section">
      <div class="location-card-fullscreen">
        <div class="location-header">
          <span class="location-icon">🏠</span>
          <h3>新家地址</h3>
        </div>
        <div class="location-address">
          <p>{{ newHomeAddress }}</p>
        </div>
        <div class="navigation-buttons">
          <button @click="openNewHomeMap" class="nav-btn gaode">
            <span class="btn-icon">🗺️</span>
            高德地图导航
          </button>
        </div>
        <div class="copy-address">
          <button @click="copyNewHomeAddress" class="copy-btn">
            <span class="btn-icon">📋</span>
            复制地址
          </button>
        </div>
      </div>
    </section>

    <!-- 第五张卡片：餐厅地址 -->
    <section class="card-section">
      <div class="location-card-fullscreen">
        <div class="location-header">
          <span class="location-icon">🍽️</span>
          <h3>餐厅地址</h3>
        </div>
        <div class="location-address">
          <p>{{ restaurantAddress }}</p>
        </div>
        <div class="navigation-buttons">
          <button @click="openRestaurantMap" class="nav-btn gaode">
            <span class="btn-icon">🗺️</span>
            高德地图导航
          </button>
        </div>
        <div class="copy-address">
          <button @click="copyRestaurantAddress" class="copy-btn">
            <span class="btn-icon">📋</span>
            复制地址
          </button>
        </div>
      </div>
    </section>

    <!-- 第六张卡片：联系信息 -->
    <section class="card-section">
      <div class="rsvp-section">
        <h3>期待您的光临</h3>
        <p class="rsvp-note">如蒙赏光，不胜感激！请于 {{ rsvpDate }} 前告知是否能够参加。</p>
        <div class="contact-info">
          <p>联系人：{{ contactName }}</p>
          <p>联系电话：{{ contactPhone }}</p>
        </div>
      </div>
    </section>

    <!-- 第七张卡片：页脚 -->
    <section class="card-section">
      <div class="invitation-footer">
        <p>{{ hostName }} 敬邀</p>
        <p class="date">{{ eventDate }}</p>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref } from 'vue'


// 配置信息（可根据实际情况修改）
const eventDate = ref('2026年4月5日')
const rsvpDate = ref('2026年4月1日')

const newHomeAddress = ref('北京市朝阳区建国路88号SOHO现代城A座')
const newHomeLatitude = ref(39.908722)
const newHomeLongitude = ref(116.458877)

const restaurantAddress = ref('北京市朝阳区国贸大酒店3楼宴会厅')
const restaurantLatitude = ref(39.908844)
const restaurantLongitude = ref(116.459141)

const hostName = ref('张三、李四')
const contactName = ref('张三')
const contactPhone = ref('138-xxxx-xxxx')

// 打开新家地图
const openNewHomeMap = () => {
  const url = `https://uri.amap.com/marker?position=${newHomeLongitude.value},${newHomeLatitude.value}&name=${encodeURIComponent('新家地址')}&coordinate=gaode`
  window.open(url, '_blank')
}

// 打开餐厅地图
const openRestaurantMap = () => {
  const url = `https://uri.amap.com/marker?position=${restaurantLongitude.value},${restaurantLatitude.value}&name=${encodeURIComponent('餐厅地址')}&coordinate=gaode`
  window.open(url, '_blank')
}

// 复制新家地址
const copyNewHomeAddress = async () => {
  try {
    await navigator.clipboard.writeText(newHomeAddress.value)
    alert('地址已复制到剪贴板！')
  } catch (err) {
    const textArea = document.createElement('textarea')
    textArea.value = newHomeAddress.value
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

// 复制餐厅地址
const copyRestaurantAddress = async () => {
  try {
    await navigator.clipboard.writeText(restaurantAddress.value)
    alert('地址已复制到剪贴板！')
  } catch (err) {
    const textArea = document.createElement('textarea')
    textArea.value = restaurantAddress.value
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
/* 容器：卡片式滚动布局 */
.invitation-container {
  width: 100%;
  height: 100%;
  overflow-y: scroll;
  scroll-snap-type: y mandatory;
  scroll-behavior: smooth;
  -webkit-overflow-scrolling: touch;
}

/* 每个section占满一屏 */
.card-section {
  width: 100%;
  min-height: 100vh;
  min-height: -webkit-fill-available;
  scroll-snap-align: start;
  scroll-snap-stop: always;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  position: relative;
}

/* 为不同的section添加背景色 - 从紫色到紫红色的线性渐变 */
.card-section:nth-child(1) {
  background: linear-gradient(135deg, #7c3aed 0%, #8b5cf6 100%);
}

.card-section:nth-child(2) {
  background: linear-gradient(135deg, #8b5cf6 0%, #a855f7 100%);
}

.card-section:nth-child(3) {
  background: linear-gradient(135deg, #a855f7 0%, #c026d3 100%);
}

.card-section:nth-child(4) {
  background: linear-gradient(135deg, #c026d3 0%, #d946ef 100%);
}

.card-section:nth-child(5) {
  background: linear-gradient(135deg, #d946ef 0%, #ec4899 100%);
}

.card-section:nth-child(6) {
  background: linear-gradient(135deg, #ec4899 0%, #db2777 100%);
}

.card-section:nth-child(7) {
  background: linear-gradient(135deg, #db2777 0%, #be185d 100%);
}

/* 第一张卡片：邀请标题 */
.invitation-header {
  text-align: center;
  color: white;
  width: 100%;
  max-width: 600px;
  padding: 80px 40px;
  padding-top: calc(80px + env(safe-area-inset-top));
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 80vh;
}

.header-decoration {
  margin-bottom: 30px;
}

.decoration-icon {
  font-size: 80px;
  display: inline-block;
  animation: bounce 2s infinite;
}

@keyframes bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}

.title {
  font-size: 56px;
  font-weight: bold;
  margin: 0 0 20px 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  letter-spacing: 8px;
}

.subtitle {
  font-size: 22px;
  margin: 0;
  opacity: 0.95;
  letter-spacing: 3px;
}

.scroll-hint {
  position: absolute;
  bottom: calc(40px + env(safe-area-inset-bottom));
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  animation: fadeInUp 2s infinite;
}

.hint-icon {
  font-size: 28px;
  margin-bottom: 8px;
}

.hint-text {
  font-size: 14px;
  opacity: 0.8;
}

@keyframes fadeInUp {
  0%, 100% {
    opacity: 0.6;
    transform: translateX(-50%) translateY(0);
  }
  50% {
    opacity: 1;
    transform: translateX(-50%) translateY(-10px);
  }
}

/* 第二张卡片：邀请内容 */
.invitation-content-card {
  text-align: center;
  color: white;
  width: 100%;
  max-width: 600px;
  padding: 80px 40px;
  padding-top: calc(80px + env(safe-area-inset-top));
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 80vh;
}

.card-icon {
  font-size: 60px;
  display: block;
  margin-bottom: 30px;
}

.invitation-content-card h2 {
  font-size: 32px;
  margin: 0 0 30px 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.message {
  font-size: 20px;
  line-height: 2;
  color: white;
  margin: 0;
  opacity: 0.95;
}

/* 第三张卡片：活动时间 */
.event-details {
  width: 100%;
  max-width: 600px;
  padding: 50px 40px;
  padding-top: calc(50px + env(safe-area-inset-top));
  padding-bottom: calc(50px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 80vh;
}

.detail-item {
  display: flex;
  align-items: center;
  padding: 50px 40px;
  margin-bottom: 40px;
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(8px);
  border-radius: 15px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.detail-item:hover {
  transform: translateY(-5px);
}

.detail-icon {
  font-size: 45px;
  margin-right: 25px;
  flex-shrink: 0;
}

.detail-content h3 {
  font-size: 24px;
  color: white;
  margin: 0 0 15px 0;
  text-shadow: 1px 1px 3px rgba(0, 0, 0, 0.2);
}

.detail-content p {
  font-size: 18px;
  color: white;
  margin: 8px 0;
  opacity: 0.95;
}

/* 第四、五张卡片：地址卡片 */
.location-card-fullscreen {
  width: 100%;
  max-width: 600px;
  padding: 50px 40px;
  padding-top: calc(50px + env(safe-area-inset-top));
  padding-bottom: calc(50px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.15);
  backdrop-filter: blur(12px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.3);
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 80vh;
}

.location-header {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.location-icon {
  font-size: 50px;
  margin-right: 20px;
}

.location-header h3 {
  font-size: 28px;
  color: white;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.location-address {
  padding: 25px;
  background: rgba(255, 255, 255, 0.2);
  backdrop-filter: blur(8px);
  border-radius: 12px;
  margin-bottom: 30px;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.location-address p {
  font-size: 20px;
  color: white;
  margin: 0;
  line-height: 1.6;
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

.navigation-buttons {
  margin-bottom: 25px;
}

.nav-btn {
  width: 100%;
  padding: 20px 24px;
  border: none;
  border-radius: 12px;
  cursor: pointer;
  font-size: 18px;
  font-weight: 500;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 12px;
  background: rgba(76, 175, 80, 0.9);
  backdrop-filter: blur(8px);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.2);
}

.btn-icon {
  font-size: 24px;
}

.nav-btn:hover {
  background: rgba(76, 175, 80, 1);
  transform: scale(1.02);
}

.copy-address {
  margin-top: 10px;
}

.copy-btn {
  width: 100%;
  padding: 18px;
  background: rgba(102, 126, 234, 0.9);
  backdrop-filter: blur(8px);
  color: white;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 12px;
  cursor: pointer;
  font-size: 17px;
  font-weight: 500;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.copy-btn:hover {
  background: rgba(102, 126, 234, 1);
  transform: scale(1.02);
}

/* 第六张卡片：联系信息 */
.rsvp-section {
  width: 100%;
  max-width: 600px;
  text-align: center;
  padding: 80px 40px;
  padding-top: calc(80px + env(safe-area-inset-top));
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 80vh;
}

.rsvp-section h3 {
  font-size: 34px;
  margin: 0 0 25px 0;
  color: white;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.2);
}

.rsvp-note {
  font-size: 19px;
  margin: 0 0 30px 0;
  opacity: 0.95;
  line-height: 1.6;
  color: white;
}

.contact-info p {
  font-size: 20px;
  margin: 12px 0;
  color: white;
  opacity: 0.95;
}

/* 第七张卡片：页脚 */
.invitation-footer {
  width: 100%;
  max-width: 600px;
  text-align: center;
  padding: 80px 40px;
  padding-top: calc(80px + env(safe-area-inset-top));
  padding-bottom: calc(80px + env(safe-area-inset-bottom));
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  display: flex;
  flex-direction: column;
  justify-content: center;
  min-height: 80vh;
}

.invitation-footer p {
  font-size: 24px;
  margin: 12px 0;
}

.date {
  font-size: 20px;
  opacity: 0.9;
}

/* 桌面端优化 */
@media (min-width: 769px) {
  .card-section {
    padding: 30px;
  }

  .invitation-header,
  .invitation-footer {
    padding: 100px 60px;
    min-height: 85vh;
  }

  .invitation-content-card,
  .rsvp-section {
    padding: 100px 60px;
    min-height: 85vh;
  }

  .event-details {
    padding: 70px 60px;
    min-height: 85vh;
  }

  .decoration-icon {
    font-size: 90px;
  }

  .title {
    font-size: 68px;
    letter-spacing: 10px;
  }

  .subtitle {
    font-size: 24px;
  }

  .card-icon {
    font-size: 70px;
  }

  .invitation-content-card h2 {
    font-size: 38px;
  }

  .message {
    font-size: 22px;
  }

  .detail-item {
    padding: 60px 50px;
    margin-bottom: 50px;
  }

  .detail-icon {
    font-size: 55px;
  }

  .detail-content h3 {
    font-size: 28px;
  }

  .detail-content p {
    font-size: 21px;
  }

  .location-card-fullscreen {
    padding: 70px 50px;
    min-height: 85vh;
  }

  .location-icon {
    font-size: 55px;
  }

  .location-header h3 {
    font-size: 32px;
  }

  .location-address {
    padding: 30px;
  }

  .location-address p {
    font-size: 22px;
  }

  .nav-btn {
    padding: 22px 28px;
    font-size: 20px;
  }

  .btn-icon {
    font-size: 26px;
  }

  .copy-btn {
    padding: 20px;
    font-size: 19px;
  }

  .rsvp-section h3 {
    font-size: 40px;
  }

  .rsvp-note {
    font-size: 21px;
  }

  .contact-info p {
    font-size: 22px;
  }

  .invitation-footer p {
    font-size: 28px;
  }

  .date {
    font-size: 22px;
  }
}

/* 移动端优化 */
@media (max-width: 600px) {
  .card-section {
    padding: 15px;
  }

  .invitation-header {
    padding: 60px 30px;
    min-height: 85vh;
  }

  .decoration-icon {
    font-size: 60px;
  }

  .title {
    font-size: 40px;
    letter-spacing: 4px;
  }

  .subtitle {
    font-size: 18px;
  }

  .scroll-hint {
    bottom: 25px;
  }

  .hint-icon {
    font-size: 24px;
  }

  .hint-text {
    font-size: 12px;
  }

  .invitation-content-card {
    padding: 60px 30px;
    min-height: 85vh;
  }

  .card-icon {
    font-size: 50px;
  }

  .invitation-content-card h2 {
    font-size: 26px;
  }

  .message {
    font-size: 18px;
    line-height: 1.8;
  }

  .event-details {
    padding: 40px 30px;
    min-height: 85vh;
  }

  .detail-item {
    flex-direction: column;
    text-align: center;
    padding: 40px 30px;
    margin-bottom: 35px;
  }

  .detail-icon {
    margin-right: 0;
    margin-bottom: 20px;
    font-size: 45px;
  }

  .detail-content h3 {
    font-size: 22px;
  }

  .detail-content p {
    font-size: 18px;
  }

  .location-card-fullscreen {
    padding: 40px 30px;
    min-height: 85vh;
  }

  .location-icon {
    font-size: 45px;
  }

  .location-header h3 {
    font-size: 24px;
  }

  .location-address {
    padding: 20px;
  }

  .location-address p {
    font-size: 18px;
  }

  .nav-btn {
    padding: 20px 15px;
    font-size: 18px;
    min-height: 60px;
  }

  .btn-icon {
    font-size: 24px;
  }

  .copy-btn {
    padding: 18px;
    font-size: 17px;
    min-height: 56px;
  }

  .rsvp-section {
    padding: 60px 30px;
    min-height: 85vh;
  }

  .rsvp-section h3 {
    font-size: 28px;
    margin-bottom: 20px;
  }

  .rsvp-note {
    font-size: 17px;
    margin-bottom: 25px;
  }

  .contact-info p {
    font-size: 18px;
  }

  .invitation-footer {
    padding: 60px 30px;
    min-height: 85vh;
  }

  .invitation-footer p {
    font-size: 20px;
  }

  .date {
    font-size: 18px;
  }
}

/* 超小屏幕优化 */
@media (max-width: 375px) {
  .invitation-header {
    padding: 50px 25px;
    min-height: 85vh;
  }

  .title {
    font-size: 34px;
    letter-spacing: 3px;
  }

  .subtitle {
    font-size: 16px;
  }

  .decoration-icon {
    font-size: 50px;
  }

  .invitation-content-card {
    padding: 50px 25px;
    min-height: 85vh;
  }

  .card-icon {
    font-size: 40px;
  }

  .invitation-content-card h2 {
    font-size: 22px;
  }

  .message {
    font-size: 16px;
  }

  .event-details {
    padding: 35px 25px;
    min-height: 85vh;
  }

  .detail-item {
    padding: 35px 25px;
  }

  .location-card-fullscreen {
    padding: 35px 25px;
    min-height: 85vh;
  }

  .location-icon {
    font-size: 40px;
  }

  .location-header h3 {
    font-size: 22px;
  }

  .location-address p {
    font-size: 16px;
  }

  .nav-btn,
  .copy-btn {
    padding: 16px;
    font-size: 16px;
  }

  .rsvp-section {
    padding: 50px 25px;
    min-height: 85vh;
  }

  .invitation-footer {
    padding: 50px 25px;
    min-height: 85vh;
  }
}

/* 横屏模式优化 */
@media (max-height: 600px) and (orientation: landscape) {
  .card-section {
    padding: 15px;
  }

  .invitation-header,
  .invitation-content-card,
  .rsvp-section,
  .invitation-footer {
    padding: 40px 30px;
    min-height: 80vh;
  }

  .event-details {
    padding: 30px;
    min-height: 80vh;
  }

  .decoration-icon {
    font-size: 45px;
  }

  .title {
    font-size: 36px;
  }

  .subtitle {
    font-size: 16px;
  }

  .scroll-hint {
    bottom: 15px;
  }

  .card-icon {
    font-size: 40px;
  }

  .invitation-content-card h2 {
    font-size: 24px;
  }

  .message {
    font-size: 16px;
  }

  .detail-item {
    padding: 30px 25px;
  }

  .detail-icon {
    font-size: 35px;
  }

  .detail-content h3 {
    font-size: 20px;
  }

  .detail-content p {
    font-size: 16px;
  }

  .location-card-fullscreen {
    padding: 35px 30px;
    min-height: 80vh;
  }

  .location-icon {
    font-size: 40px;
  }

  .location-header h3 {
    font-size: 22px;
  }

  .location-address {
    padding: 18px;
  }

  .location-address p {
    font-size: 16px;
  }

  .nav-btn {
    padding: 16px;
    font-size: 16px;
  }

  .btn-icon {
    font-size: 20px;
  }

  .copy-btn {
    padding: 14px;
    font-size: 15px;
  }

  .rsvp-section h3 {
    font-size: 26px;
    margin-bottom: 15px;
  }

  .rsvp-note {
    font-size: 16px;
    margin-bottom: 18px;
  }

  .contact-info p {
    font-size: 17px;
  }

  .invitation-footer p {
    font-size: 18px;
  }
}
</style>
