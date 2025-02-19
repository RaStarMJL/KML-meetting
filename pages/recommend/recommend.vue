<script setup lang="ts">
import { ref } from 'vue';
import NavBar from "./components/NavBar.vue";

const defaultAvatar = '/src/static/icons/tab/ok.png';

// 轮播图数据
const swiperList = ref([
  {
    id: 1,
    image: '/static/images/banner1.jpg',
    title: '2024技术峰会'
  },
  {
    id: 2,
    image: '/static/images/banner2.jpg',
    title: 'AI发展论坛'
  },
  {
    id: 3,
    image: '/static/images/banner3.jpg',
    title: '创新创业大会'
  }
]);

// 推荐会议数据
const recommendList = ref([
  {
    id: 1,
    title: '普现急速摸卡流',
    views: '1381',
    duration: '1:30:00',
    cover: '/static/images/meeting1.jpg'
  },
  {
    id: 2,
    title: '从来如此，便对么？',
    views: '302.1万',
    duration: '2:59',
    cover: '/static/images/meeting2.jpg'
  },
  {
    id: 3,
    title: 'STM32智能大棚项目',
    views: '2078',
    duration: '7:31',
    cover: '/static/images/meeting3.jpg'
  },
  {
    id: 4,
    title: '洛克王国开发进度分享',
    views: '293.2万',
    duration: '1:49',
    cover: '/static/images/meeting4.jpg'
  },
  {
    id: 5,
    title: '2024前端技术分享会',
    views: '5.2万',
    duration: '45:21',
    cover: '/static/images/meeting5.jpg'
  },
  {
    id: 6,
    title: 'AI助手开发经验分享',
    views: '12.5万',
    duration: '32:15',
    cover: '/static/images/meeting6.jpg'
  },
  {
    id: 7,
    title: '区块链技术应用实践',
    views: '8.9万',
    duration: '1:15:00',
    cover: '/static/images/meeting7.jpg'
  },
  {
    id: 8,
    title: '移动应用性能优化',
    views: '6.7万',
    duration: '55:30',
    cover: '/static/images/meeting8.jpg'
  },
  {
    id: 9,
    title: '云原生架构设计',
    views: '15.3万',
    duration: '1:20:00',
    cover: '/static/images/meeting9.jpg'
  },
  {
    id: 10,
    title: '微服务部署与运维',
    views: '9.4万',
    duration: '48:25',
    cover: '/static/images/meeting10.jpg'
  }
]);

// 控制返回顶部按钮的显示/隐藏
const showBackTop = ref(false);
const scrollTop = ref(0);

// scroll-view 的滚动事件处理
const onScroll = (e: any) => {
  scrollTop.value = e.detail.scrollTop;
  showBackTop.value = e.detail.scrollTop > 0;
};

// 返回顶部方法
const backToTop = () => {
  scrollTop.value = 0;
};

// fab 按钮配置，简化为单个按钮
const fabPattern = {
  color: '#0052d9',
  backgroundColor: '#fff',
  selectedColor: '#0052d9',
  buttonColor: '#0052d9'
};
</script>

<template>
  <view class="page-container">
    <!-- 固定头部 -->
    <view class="header">
      <!-- 搜索栏 -->
      <view class="search-bar">
        <image :src="defaultAvatar" class="user-avatar"></image>
        <view class="search-input">
          <uni-icons type="search" size="20" color="#666"></uni-icons>
          <input type="text" placeholder="搜索会议" />
        </view>
        <uni-icons type="videocam" size="24" color="#666"></uni-icons>
        <uni-icons type="email" size="24" color="#666"></uni-icons>
      </view>

      <!-- 导航栏 -->
      <view class="nav-bar">
        <view class="nav-item active">推荐</view>
        <view class="nav-item">热门</view>
        <view class="nav-item">直播</view>
        <view class="nav-item">会议</view>
        <view class="nav-item">盛典</view>
      </view>
    </view>

    <!-- 滚动内容区域 -->
    <scroll-view 
      scroll-y 
      class="content-scroll"
      :scroll-top="scrollTop"
      @scrolltolower="loadMore"
      refresher-enabled
      @refresherrefresh="onRefresh"
      @scroll="onScroll"
      scroll-with-animation
    >
      <!-- 轮播图 -->
      <swiper class="banner-swiper" circular :indicator-dots="true" :autoplay="true" interval="3000" duration="1000">
        <swiper-item v-for="item in swiperList" :key="item.id">
          <view class="banner-item">
            <image :src="item.image" mode="aspectFill"></image>
            <view class="banner-title">{{ item.title }}</view>
          </view>
        </swiper-item>
      </swiper>

      <!-- 会议推荐网格 -->
      <view class="meeting-grid">
        <view class="meeting-item" v-for="item in recommendList" :key="item.id">
          <view class="meeting-cover">
            <image :src="item.cover" mode="aspectFill"></image>
            <view class="meeting-duration">{{ item.duration }}</view>
          </view>
          <view class="meeting-info">
            <view class="meeting-title">{{ item.title }}</view>
            <view class="meeting-views">
              <uni-icons type="eye" size="12" color="#999"></uni-icons>
              <text>{{ item.views }}</text>
            </view>
          </view>
        </view>
      </view>
    </scroll-view>

    <!-- 简单的返回顶部按钮 -->
    <view 
      v-show="showBackTop" 
      class="back-to-top"
      @click="backToTop"
    >
      <uni-icons type="top" size="20" color="#fff"></uni-icons>
    </view>
  </view>
</template>

<style scoped>
.page-container {
  display: flex;
  flex-direction: column;
  height: 100vh;
}

.header {
  background-color: #fff;
  z-index: 100;
}

.search-bar {
  display: flex;
  align-items: center;
  padding: 20rpx;
  background-color: #fff;
}

.user-avatar {
  width: 60rpx;
  height: 60rpx;
  border-radius: 50%;
  margin-right: 20rpx;
}

.search-input {
  flex: 1;
  display: flex;
  align-items: center;
  background-color: #f5f6f7;
  border-radius: 32rpx;
  padding: 12rpx 24rpx;
  margin-right: 20rpx;
}

.search-input input {
  flex: 1;
  margin-left: 16rpx;
  font-size: 28rpx;
}

.nav-bar {
  display: flex;
  justify-content: space-around;
  padding: 20rpx 0;
  border-bottom: 1rpx solid #eee;
}

.nav-item {
  font-size: 28rpx;
  color: #666;
  padding: 0 20rpx;
}

.nav-item.active {
  color: #0052d9;
  font-weight: bold;
  position: relative;
}

.nav-item.active::after {
  content: '';
  position: absolute;
  bottom: -10rpx;
  left: 50%;
  transform: translateX(-50%);
  width: 40rpx;
  height: 4rpx;
  background-color: #0052d9;
  border-radius: 2rpx;
}

.content-scroll {
  flex: 1;
  background-color: #f5f6f7;
}

.banner-swiper {
  height: 300rpx;
  margin: 20rpx;
}

.banner-item {
  position: relative;
  width: 100%;
  height: 100%;
  border-radius: 12rpx;
  overflow: hidden;
}

.banner-item image {
  width: 100%;
  height: 100%;
}

.banner-title {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  padding: 20rpx;
  background: linear-gradient(transparent, rgba(0,0,0,0.7));
  color: #fff;
  font-size: 28rpx;
}

.meeting-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20rpx;
  padding: 20rpx;
}

.meeting-item {
  background-color: #fff;
  border-radius: 12rpx;
  overflow: hidden;
}

.meeting-cover {
  position: relative;
  width: 100%;
  height: 200rpx;
}

.meeting-cover image {
  width: 100%;
  height: 100%;
}

.meeting-duration {
  position: absolute;
  bottom: 10rpx;
  right: 10rpx;
  background-color: rgba(0,0,0,0.6);
  color: #fff;
  font-size: 24rpx;
  padding: 4rpx 8rpx;
  border-radius: 4rpx;
}

.meeting-info {
  padding: 16rpx;
}

.meeting-title {
  font-size: 26rpx;
  color: #333;
  margin-bottom: 8rpx;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}

.meeting-views {
  display: flex;
  align-items: center;
  font-size: 24rpx;
  color: #999;
}

.meeting-views text {
  margin-left: 6rpx;
}

/* 返回顶部按钮样式 */
.back-to-top {
  position: fixed;
  right: 30rpx;
  bottom: 120rpx;
  width: 80rpx;
  height: 80rpx;
  border-radius: 50%;
  background-color: #0052d9;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 2px 8px rgba(0,0,0,0.15);
  z-index: 99;
}
</style>
