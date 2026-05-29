<script lang="ts" setup>
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import Tabbar from '@/components/Tabbar.vue'
import { getImage } from '@/utils/imageManager'
import PLATFORM from '@/utils/platform'
//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const { navBarInfo } = useUniAppSystemRectInfo()

const settingList = ref([
  {
    icon: getImage('mineList1'),
    path: '/pages/mine/appSetting',
    title: '我的医生团队',
  },
  {
    icon: getImage('mineList2'),
    path: '/pages/mine/appSetting',
    title: '签约管理',
  },
  {
    icon: getImage('mineList3'),
    path: '/pages/mine/appSetting',
    title: '服务管理',
  },
  {
    icon: getImage('mineList4'),
    path: '/pages/mine/appSetting',
    title: '使用指南',
  },
  {
    icon: getImage('mineList5'),
    path: '/pages/mine/appSetting',
    title: '设置',
  },
])

function handleSettingItemClick(item: { path: string }) {
  uni.navigateTo({
    url: item.path,
  })
}

function pageToScanQrcode() {
  uni.navigateTo({
    url: '/pages/mine/scanQrcode',
  })
}
</script>

<template>
  <view class="">
    <view class="bg-#49B9AD">
      <view>
        <view :style="{ height: navBarInfo.height + 'px' }"></view>
        <view class="flex justify-end">
          <view
            class="h-8.25 w-18.75 flex items-center justify-center rounded-l-full bg-[rgba(0,0,0,.15)] px-3.25 color-#fff"
          >
            切换团队
          </view>
        </view>
      </view>

      <view class="z-2 mx-3 mt-4 rounded-t-2.5 bg-#fff py-3.75">
        <!--头像 -->
        <view class="flex items-center justify-between px-3.75">
          <view class="flex items-center">
            <image class="h-15 w-15 rounded-full" :src="getImage('mineAvatar')" />
            <view class="ml-3.75 h-15 flex flex-col py-2.5">
              <view class="text-4 color-#333 line-height-none">张三四</view>
              <image class="ml--1.5 mt-2 h-5.25 w-17.5 shrink-0" :src="getImage('mineUserTag')" />
            </view>
          </view>
          <image class="h-5 w-5" :src="getImage('mineQrcode')" @click="pageToScanQrcode" />
        </view>
      </view>
    </view>
    <!-- 信息标签 -->
    <view class="mx-3 mt-3.25 h-17 flex flex items-center bg-#F8FFFD">
      <view class="flex flex-1 items-center justify-center">
        <image class="h-4.5 w-4.5" :src="getImage('mineTag1')" />
        <view class="ml-2">
          <view class="line-height-none">所属团队</view>
          <view class="mt-1 color-#606972 line-height-none">阳兰广专科团队</view>
        </view>
      </view>
      <view class="h-5 w-1px bg-#E3E4E5"></view>
      <view class="flex flex-1 items-center justify-center">
        <image class="h-4.5 w-4.5" :src="getImage('mineTag2')" />
        <view class="ml-2">
          <view class="line-height-none">所属机构</view>
          <view class="mt-1 color-#606972 line-height-none">桂雅卫生服务站</view>
        </view>
      </view>
    </view>

    <!-- 列表 -->
    <view class="mt-3.75 px-3">
      <view
        v-for="(item, index) in settingList"
        :key="index"
        class="flex justify-between border-0 border-b border-#E3E4E5 border-solid py-4"
        @click="handleSettingItemClick(item)"
      >
        <view class="ml-1.75 flex items-center">
          <image class="h-3.75 w-3.75" :src="item.icon" />
          <view class="ml-2.5 text-3.75">{{ item.title }}</view>
        </view>
        <image class="mr-1.75 h-2.5 w-2.5" :src="getImage('commonArrowRight')" />
      </view>
    </view>
    <Tabbar tabbarPath="/pages/mine/mine" />
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '我的',
  },
  needLogin: false,
}
</route>
