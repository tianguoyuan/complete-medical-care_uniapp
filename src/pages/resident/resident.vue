<script lang="ts" setup>
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import Tabbar from '@/components/Tabbar.vue'
import PLATFORM from '@/utils/platform'
//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const { navBarInfo } = useUniAppSystemRectInfo()
</script>

<template>
  <view class="">
    <Tabbar tabbar-path="/pages/resident/resident" />
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'default',
    navigationBarTitleText: '居民',
  },
  needLogin: false,
}
</route>
