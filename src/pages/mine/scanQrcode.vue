<script lang="ts" setup>
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'
const { navBarInfo } = useUniAppSystemRectInfo()

const appStore = useAppStore()
function back() {
  uni.navigateBack()
}
//
</script>

<template>
  <view
    class=""
    :style="{ minHeight: appStore.systemScreenHeight + 'px', backgroundColor: '#D8F2FC' }"
  >
    <view
      :style="{
        height: navBarInfo.height + 'px',
      }"
    ></view>
    <view
      class="h-6.25 w-12.5 flex items-center justify-center rounded-r-full bg-#C7EAEC color-#49B9AD"
      @click="back"
    >
      返回
    </view>
    <view class="px-3">
      <image class="h-60 w-full" :src="getImage('mineScanQrcodeBgCover')" />
    </view>
    <view class="mx-3 rounded-2.5 bg-#fff p-6.25 shadow-#C6D0D3">
      <!--头像 -->
      <view class="flex items-center justify-between">
        <view class="flex items-center">
          <image class="h-15 w-15 rounded-full" :src="getImage('mineAvatar')" />
          <view class="ml-3.75 h-15 flex flex-col py-2.5">
            <view class="text-4 color-#333 line-height-none">张三四</view>
            <image class="ml--1.5 mt-2 h-5.25 w-17.5 shrink-0" :src="getImage('mineUserTag')" />
          </view>
        </view>
      </view>

      <view class="mt-3.75 h-6.75 flex items-center rounded-1.25 bg-#EAFEFA pl-2.5 color-#49B9AD">
        所属团队：李明明专科团队
      </view>

      <view class="mt-3.75 h-6.75 flex items-center rounded-1.25 bg-#EAFEFA pl-2.5 color-#49B9AD">
        所属机构：佛山市桂雅社区卫生服务站
      </view>
      <view class="mt-11.25 text-center">
        <image class="h-50 w-50" :src="getImage('mineQrcode')" />
        <view class="mt-6.25">扫一扫，快速签约医生团队</view>
      </view>
    </view>
    <view class="h-10 pb-safe"></view>
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
    navigationBarTitleText: '扫码签约',
  },
}
</route>
