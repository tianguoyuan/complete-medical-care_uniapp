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
</script>

<template>
  <view class="">
    <view class="bg-#49B9AD h-48.5 relative">
      <view
        class="absolute right-0 color-#fff h-8.25 rounded-l-full bg-[rgba(0,0,0,.15)] px-3.25 flex justify-center items-center"
        :style="{ top: navBarInfo.statusHeight + 24 + 'px' }"
      >
        切换团队
      </view>
    </view>

    <view class="bg-#fff mt--23.75 rounded-t-2.5 relative z-2 mx-3 py-3.75">
      <!--头像 -->
      <view class="flex justify-between items-center px-3.75">
        <view class="flex items-center">
          <image class="w-15 h-15 rounded-full" :src="getImage('mineAvatar')" />
          <view class="ml-3.75 flex flex-col py-2.5 h-15">
            <view class="color-#333 text-4 line-height-none">张三四</view>
            <image class="w-17.5 h-5.25 mt-2 ml--1.5 shrink-0" :src="getImage('mineUserTag')" />
          </view>
        </view>
        <image class="w-5 h-5" :src="getImage('mineQrcode')" />
      </view>

      <!-- 信息标签 -->
      <view class="mt-3.25 flex bg-#F8FFFD h-17 flex items-center">
        <view class="flex-1 flex justify-center items-center">
          <image class="h-4.5" mode="heightFix" :src="getImage('mineTag1')" />
          <view class="ml-2">
            <view class="line-height-none">所属团队</view>
            <view class="color-#606972 mt-1 line-height-none">阳兰广专科团队</view>
          </view>
        </view>
        <view class="h-5 w-1px bg-#E3E4E5"></view>
        <view class="flex-1 flex justify-center items-center">
          <image class="h-4.5" mode="heightFix" :src="getImage('mineTag2')" />
          <view class="ml-2">
            <view class="line-height-none">所属机构</view>
            <view class="color-#606972 mt-1 line-height-none">桂雅卫生服务站</view>
          </view>
        </view>
      </view>

      <!-- 列表 -->
      <view class="mt-3.75 px-2.5">
        <view
          v-for="(item, index) in settingList"
          :key="index"
          class="flex justify-between py-4 border-0 border-b border-#E3E4E5 border-solid"
          @click="handleSettingItemClick(item)"
        >
          <view class="flex items-center ml-1.75">
            <image class="w-3.75" mode="widthFix" :src="item.icon" />
            <view class="ml-2.5 text-3.75">{{ item.title }}</view>
          </view>
          <image class="h-2.5 mr-1.75" mode="heightFix" :src="getImage('commonArrowRight')" />
        </view>
      </view>
    </view>
    <Tabbar tabbar-path="/pages/mine/mine" />
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
