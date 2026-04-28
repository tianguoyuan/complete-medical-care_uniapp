<script lang="ts" setup>
import PLATFORM from '@/utils/platform'
import Tabbar from '@/components/Tabbar.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'
//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const { navBarInfo } = useUniAppSystemRectInfo()
</script>

<template>
  <view class="">
    <Tabbar tabbar-path="/pages/mine/mine" />
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'default',
    navigationBarTitleText: '首页',
  },
  needLogin: false,
}
</route>
