<script lang="ts" setup>
import { useUserStore } from '@/store'
import { getImage } from '@/utils/imageManager'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

const { systemScreenInfo } = useUniAppSystemRectInfo()
const userStore = useUserStore()
const appSettingList = ref([
  {
    title: '个人资料',
    rightIcon: getImage('commonArrowRight'),
  },
  {
    title: '修改密码',
    rightIcon: getImage('commonArrowRight'),
  },
  {
    title: '消息通知',
    switchBtn: true,
  },
  {
    title: '清除缓存',
    rightText: '6.4M',
    rightIcon: getImage('commonArrowRight'),
  },
  {
    title: '升级版本',
    rightText: '当前版本1.01.1',
    rightIcon: getImage('commonArrowRight'),
  },
  {
    title: '关于我们',
    rightIcon: getImage('commonArrowRight'),
  },
])
function handleLogout() {
  userStore.clearUserInfo()
  uni.reLaunch({
    url: '/pages/user/login',
  })
}
//
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: systemScreenInfo.height + 'px' }">
    <view v-for="(item, index) in appSettingList" :key="index" class="bg-white">
      <view
        class="flex items-center justify-between py-4 mx-4 border-0 border-b border-#E3E4E5 border-solid"
      >
        <text class="text-3.75 text-gray-800">{{ item.title }}</text>
        <view class="flex items-center">
          <text v-if="item.rightText" class="mr-2.5 color-#C5C8CB">{{ item.rightText }}</text>
          <image v-if="item.rightIcon" :src="item.rightIcon" class="h2.5" mode="heightFix" />
        </view>
      </view>
    </view>

    <view
      class="mt-12.5 color-#49B9AD border border-#49B9AD border-solid rounded-2.5 h-10 flex justify-center items-center mx-3 text-3.75"
      @click="handleLogout"
    >
      退出账号
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
    navigationStyle: 'default',
    navigationBarTitleText: '设置',
  },
}
</route>
