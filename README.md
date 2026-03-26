# 乔迁请帖 🏠

一个精美的电子乔迁请帖应用，使用 Vue 3 开发，支持地图导航功能。

## 功能特性

✨ **精美的视觉设计**
- 渐变色背景和卡片设计
- 响应式布局，支持手机和电脑访问
- 流畅的动画效果

📍 **位置导航**
- 支持高德地图、百度地图、腾讯地图导航
- 一键复制地址功能
- 预留新家地址和餐厅地址

📱 **易于分享**
- 可部署到 GitHub Pages
- 生成链接后可直接分享给亲友

## 快速开始

### 安装依赖

```sh
npm install
```

### 开发模式

```sh
npm run dev
```

访问 http://localhost:5173 查看效果

### 生产构建

```sh
npm run build
```

## 自定义配置

### 修改请帖信息

编辑 `src/components/HousewarmingInvitation.vue` 文件中的配置信息：

```javascript
// 活动信息
const eventName = ref('乔迁之喜')
const eventDate = ref('2026年4月5日')  // 修改为您的活动日期
const rsvpDate = ref('2026年4月1日')   // 修改为回复截止日期

// 新家地址
const newHomeAddress = ref('北京市朝阳区建国路88号SOHO现代城A座')
const newHomeLatitude = ref(39.908722)   // 修改为实际纬度
const newHomeLongitude = ref(116.458877) // 修改为实际经度

// 餐厅地址
const restaurantAddress = ref('北京市朝阳区国贸大酒店3楼宴会厅')
const restaurantLatitude = ref(39.908844)  // 修改为实际纬度
const restaurantLongitude = ref(116.459141) // 修改为实际经度

// 联系信息
const hostName = ref('张三、李四')        // 修改为主人姓名
const contactName = ref('张三')           // 修改为联系人姓名
const contactPhone = ref('138-xxxx-xxxx') // 修改为联系电话
```

### 如何获取地址的经纬度？

1. **高德地图**：打开 [高德地图坐标拾取器](https://lbs.amap.com/tools/picker)
2. **百度地图**：打开 [百度地图坐标拾取系统](http://api.map.baidu.com/lbsapi/getpoint/index.html)
3. **腾讯地图**：打开 [腾讯地图坐标拾取器](https://lbs.qq.com/tool/getpoint/index.html)

## 部署到 GitHub Pages

### 方法一：使用 npm 脚本（推荐）

1. 在 GitHub 上创建一个新仓库，仓库名为 `housewarming-invitation`

2. 修改 `vite.config.js` 中的 `base` 配置：
   ```javascript
   base: '/housewarming-invitation/',  // 替换为您的仓库名
   ```

3. 推送代码到 GitHub：
   ```sh
   git remote add origin https://github.com/YOUR_USERNAME/housewarming-invitation.git
   git branch -M main
   git push -u origin main
   ```

4. 部署到 GitHub Pages：
   ```sh
   npm run deploy
   ```

5. 访问您的请帖：
   ```
   https://YOUR_USERNAME.github.io/housewarming-invitation/
   ```

### 方法二：手动部署

1. 构建项目：
   ```sh
   npm run build
   ```

2. 在 GitHub 仓库设置中，找到 "Pages" 选项

3. 在 "Source" 下选择 "Deploy from a branch"

4. 选择 `gh-pages` 分支作为部署源

## 项目结构

```
housewarming-invitation/
├── src/
│   ├── components/
│   │   ├── HousewarmingInvitation.vue  # 主请帖组件
│   │   └── LocationCard.vue            # 地址卡片组件
│   ├── App.vue                         # 根组件
│   └── main.js                         # 入口文件
├── public/                             # 静态资源
├── index.html                          # HTML 模板
├── vite.config.js                      # Vite 配置
└── package.json                        # 项目配置
```

## 技术栈

- **Vue 3** - 渐进式 JavaScript 框架
- **Vite** - 下一代前端构建工具
- **GitHub Pages** - 静态网站托管服务

## 浏览器支持

- Chrome (推荐)
- Firefox
- Safari
- Edge

## 开发建议

### IDE 设置

推荐使用 [VS Code](https://code.visualstudio.com/) + [Vue - Official](https://marketplace.visualstudio.com/items?itemName=Vue.volar) 扩展。

### 浏览器开发工具

- [Vue.js devtools](https://chromewebstore.google.com/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd) (Chrome/Edge)
- [Vue.js devtools](https://addons.mozilla.org/en-US/firefox/addon/vue-js-devtools/) (Firefox)

## 许可证

MIT License

## 贡献

欢迎提交 Issue 和 Pull Request！

---

祝您乔迁大吉！🎉🏠
