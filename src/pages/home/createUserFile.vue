<script lang="ts" setup>
import Navbar from '@/components/Navbar.vue'

//
</script>

<template>
  <view class="">
    <Navbar title="新建居民档案" showBackIcon />

    <view class="px-3">
      <view class="py-3.75 text-4">居民基本信息</view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '新建居民档案',
  },
}
</route>
