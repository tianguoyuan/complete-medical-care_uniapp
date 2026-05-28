<script lang="ts" setup>
import Navbar from '@/components/Navbar.vue'

//
</script>

<template>
  <view class="">
    <Navbar fixed showBackIcon showHomeIcon title="服务管理" />
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
    navigationBarTitleText: '服务管理',
  },
}
</route>
