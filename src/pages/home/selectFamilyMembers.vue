<script lang="ts" setup>
import Navbar from '@/components/Navbar.vue'
//
</script>

<template>
  <view class="">
    <Navbar fixed show-back-icon title="新建居民档案" />
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
    navigationBarTitleText: '选择家庭成员',
  },
}
</route>
