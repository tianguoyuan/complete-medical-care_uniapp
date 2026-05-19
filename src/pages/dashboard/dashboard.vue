<script lang="ts" setup>
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import { useUserStore } from '@/store'
import { getImage } from '@/utils/imageManager'
const rectInfo = useUniAppSystemRectInfo()

const count = ref(5)

// 倒计时
const timer = setInterval(() => {
  if (count.value <= 0) {
    clearInterval(timer)
    return
  }
  count.value--
}, 1000)

onUnmounted(() => {
  clearInterval(timer)
})

const userStore = useUserStore()
function pageToHome() {
  if (count.value > 0) clearInterval(timer)

  if (userStore.isLogin) {
    uni.switchTab({
      url: '/pages/home/home',
    })
  } else {
    uni.navigateTo({
      url: '/pages/user/login',
    })
  }
}
</script>

<template>
  <view>
    <view :style="{ height: rectInfo.navBarInfo.height + 'px' }"></view>
    <view class="px-6 relative">
      <view
        class="bg-[#6A6D6F] rounded-1.25 px-3.5 color-#fff absolute right-6 h-7.5 flex items-center"
        @click="pageToHome"
      >
        <text>跳过</text>
        <text v-if="count !== 0" class="ml-0.5">{{ count }}</text>
      </view>
      <image class="w-full mt-16 px-2" mode="widthFix" :src="getImage('dashboardCover')" />
    </view>
    <view class="absolute flex justify-center w-full bottom-13">
      <image class="h-7.75 w-40.5" :src="getImage('dashboardTitle')" />
      <view class="pb-safe bg-#f99"></view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>

<route lang="json5" type="home">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '引导页',
  },
}
</route>
