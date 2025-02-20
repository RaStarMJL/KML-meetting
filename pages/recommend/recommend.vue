<script setup>
import { ref } from "vue";
import NavBar from "./components/NavBar.vue";
import NavSwiper from "./components/NavSwiper.vue";
const list = ref([]);
list.value = [
  {
    id: "21",
    imgUrl: "/static/images/swiper/1.jpg",
    hrefUrl: "1005000",
    type: "1",
  },
  {
    id: "25",
    imgUrl: "/static/images/swiper/2.jpg",
    hrefUrl: "1005000",
    type: "1",
  },
  {
    id: "22",
    imgUrl: "/static/images/swiper/3.jpg",
    hrefUrl: "1019000",
    type: "1",
  },
  {
    id: "24",
    imgUrl: "/static/images/swiper/4.png",
    hrefUrl: "1013001",
    type: "1",
  },
  {
    id: "23",
    imgUrl: "/static/images/swiper/5.png",
    hrefUrl: "1013001",
    type: "1",
  },
];
</script>
<template>
  <NavBar></NavBar>
  <scroll-view
    refresher-enabled
    @refresherrefresh="onRefresherrefresh"
    :refresher-triggered="isTriggered"
    class="scroll-view"
    scroll-y
    @scrolltolower="onScrolltolower">
    <NavSwiper :list="list" class="swiper"></NavSwiper>
  </scroll-view>
  <div>这是recommend</div>
</template>
<style scoped lang="scss">
.swiper {
  height: 250rpx;
}
</style>
