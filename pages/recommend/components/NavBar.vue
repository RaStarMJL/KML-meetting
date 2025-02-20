<script lang="ts" setup>
const { safeAreaInsets } = uni.getSystemInfoSync();
const confirm = () => {
  console.log("confirm");
};
</script>

<template>
  <view class="box-bg" :style="{ paddingTop: safeAreaInsets?.top + 'px' }">
    <uni-nav-bar
      leftWidth="50rpx"
      rightWidth="50rpx"
      leftIcon="contact"
      rightIcon="email"
      border="false">
      <view class="input-view">
        <uni-icons
          class="input-uni-icon"
          type="search"
          size="18"
          color="#999" />
        <input
          confirm-type="search"
          class="nav-bar-input"
          type="text"
          placeholder="输入搜索关键词"
          @confirm="confirm" />
      </view>
    </uni-nav-bar>
  </view>
</template>
<style lang="scss">
$nav-height: 30px;

.box-bg {
  background-color: #f5f5f5;
  padding: 5px 0;
}

.city {
  /* #ifndef APP-PLUS-NVUE */
  display: flex;
  /* #endif */
  flex-direction: row;
  align-items: center;
  justify-content: flex-start;
  // width: 160rpx;
  margin-left: 4px;
}

.input-view {
  /* #ifndef APP-PLUS-NVUE */
  display: flex;
  /* #endif */
  flex-direction: row;
  // width: 500rpx;
  flex: 1;
  background-color: #f8f8f8;
  height: $nav-height;
  border-radius: 15px;
  padding: 0 15px;
  flex-wrap: nowrap;
  margin: 7px 0;
  line-height: $nav-height;
}

.input-uni-icon {
  line-height: $nav-height;
}

.nav-bar-input {
  height: $nav-height;
  line-height: $nav-height;
  /* #ifdef APP-PLUS-NVUE */
  width: 370rpx;
  /* #endif */
  padding: 0 5px;
  font-size: 12px;
  background-color: #f8f8f8;
}
</style>
