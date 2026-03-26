<template>
  <div class="invitation">
    <div class="invitation-header">
      <div class="header-decoration">
        <span class="decoration-icon">🏠</span>
      </div>
      <h1 class="title">乔迁之喜</h1>
      <p class="subtitle">诚挚邀请您共襄盛举</p>
    </div>

    <div class="invitation-content">
      <div class="invitation-card">
        <div class="card-header">
          <span class="card-icon">🎉</span>
          <h2>亲爱的亲朋好友</h2>
        </div>
        <p class="message">
          良辰吉日，乔迁新居！<br />
          在这个喜庆的日子里，我们诚挚地邀请您来参加我们的乔迁宴会，<br />
          与我们共同分享这份喜悦！
        </p>
      </div>

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

      <div class="locations">
        <LocationCard
          title="新家地址"
          :address="newHomeAddress"
          icon="🏠"
          :latitude="newHomeLatitude"
          :longitude="newHomeLongitude"
        />
        <LocationCard
          title="餐厅地址"
          :address="restaurantAddress"
          icon="🍽️"
          :latitude="restaurantLatitude"
          :longitude="restaurantLongitude"
        />
      </div>

      <div class="rsvp-section">
        <h3>期待您的光临</h3>
        <p class="rsvp-note">如蒙赏光，不胜感激！请于 {{ rsvpDate }} 前告知是否能够参加。</p>
        <div class="contact-info">
          <p>联系人：{{ contactName }}</p>
          <p>联系电话：{{ contactPhone }}</p>
        </div>
      </div>
    </div>

    <div class="invitation-footer">
      <p>{{ hostName }} 敬邀</p>
      <p class="date">{{ eventDate }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import LocationCard from './LocationCard.vue'

// 配置信息（可根据实际情况修改）
const eventName = ref('乔迁之喜')
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
</script>

<style scoped>
.invitation {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 20px;
  box-shadow: 0 10px 40px rgba(0, 0, 0, 0.2);
}

.invitation-header {
  text-align: center;
  padding: 40px 20px;
  color: white;
}

.header-decoration {
  margin-bottom: 20px;
}

.decoration-icon {
  font-size: 60px;
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
  font-size: 48px;
  font-weight: bold;
  margin: 0;
  text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
  letter-spacing: 8px;
}

.subtitle {
  font-size: 18px;
  margin-top: 10px;
  opacity: 0.9;
  letter-spacing: 2px;
}

.invitation-content {
  background: white;
  border-radius: 15px;
  padding: 30px;
  margin-top: 20px;
}

.invitation-card {
  text-align: center;
  padding: 30px;
  background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
  border-radius: 12px;
  margin-bottom: 30px;
}

.card-header {
  margin-bottom: 20px;
}

.card-icon {
  font-size: 40px;
  display: block;
  margin-bottom: 10px;
}

.card-header h2 {
  font-size: 24px;
  color: #2c3e50;
  margin: 0;
}

.message {
  font-size: 16px;
  line-height: 1.8;
  color: #555;
  margin: 0;
}

.event-details {
  margin-bottom: 30px;
}

.detail-item {
  display: flex;
  align-items: flex-start;
  padding: 20px;
  background: #f8f9fa;
  border-radius: 12px;
  margin-bottom: 15px;
  transition: transform 0.3s ease;
}

.detail-item:hover {
  transform: translateX(5px);
}

.detail-icon {
  font-size: 32px;
  margin-right: 15px;
  flex-shrink: 0;
}

.detail-content h3 {
  font-size: 18px;
  color: #2c3e50;
  margin: 0 0 10px 0;
}

.detail-content p {
  font-size: 15px;
  color: #666;
  margin: 5px 0;
}

.locations {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  margin-bottom: 30px;
}

.rsvp-section {
  text-align: center;
  padding: 30px;
  background: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
  border-radius: 12px;
  color: white;
}

.rsvp-section h3 {
  font-size: 24px;
  margin: 0 0 15px 0;
}

.rsvp-note {
  font-size: 15px;
  margin: 0 0 20px 0;
  opacity: 0.95;
}

.contact-info p {
  font-size: 16px;
  margin: 5px 0;
}

.invitation-footer {
  text-align: center;
  padding: 30px 20px;
  color: white;
}

.invitation-footer p {
  font-size: 18px;
  margin: 5px 0;
}

.date {
  font-size: 16px;
  opacity: 0.9;
}

@media (max-width: 600px) {
  .invitation {
    margin: 10px;
    padding: 15px;
  }

  .title {
    font-size: 36px;
    letter-spacing: 4px;
  }

  .subtitle {
    font-size: 16px;
  }

  .invitation-content {
    padding: 20px;
  }

  .detail-item {
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .detail-icon {
    margin-right: 0;
    margin-bottom: 10px;
  }
}
</style>
