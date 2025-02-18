<script lang="ts" setup>
import { ref } from "vue";
const title = ref();
title.value = "推荐";
</script>

<template>
  <uni-nav-bar :title="title"></uni-nav-bar>
</template>
