<script lang="ts" setup>
import type { TnModalInstance } from '@tuniao/tnui-vue3-uniapp/components/modal'

import TnModal from '@tuniao/tnui-vue3-uniapp/components/modal/src/modal.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import { useUserStore } from '@/store'
import { getImage } from '@/utils/imageManager'

const { systemScreenInfo } = useUniAppSystemRectInfo()
const userStore = useUserStore()
const modalRef = ref<TnModalInstance>()

const appSettingList = ref([
  {
    rightIcon: getImage('commonArrowRight'),
    title: '个人资料',
  },
  {
    rightIcon: getImage('commonArrowRight'),
    title: '修改密码',
  },
  {
    switchBtn: true,
    title: '消息通知',
  },
  {
    rightIcon: getImage('commonArrowRight'),
    rightText: '6.4M',
    title: '清除缓存',
  },
  {
    rightIcon: getImage('commonArrowRight'),
    rightText: '当前版本1.01.1',
    title: '升级版本',
  },
  {
    rightIcon: getImage('commonArrowRight'),
    title: '关于我们',
  },
])
function handleLogout() {
  modalRef.value?.showModal({
    confirm() {
      userStore.clearUserInfo()
      uni.reLaunch({
        url: '/pages/user/login',
      })
    },
    content: '是否退出登录？',
    showCancel: true,
    title: '提示',
  })
}
//
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: systemScreenInfo.height + 'px' }">
    <TnModal ref="modalRef" />
    <view v-for="(item, index) in appSettingList" :key="index" class="bg-white">
      <view
        class="flex items-center justify-between py-4 mx-4 border-0 border-b border-#E3E4E5 border-solid"
      >
        <text class="text-3.75 text-gray-800">{{ item.title }}</text>
        <view class="flex items-center">
          <text v-if="item.rightText" class="mr-2.5 color-#C5C8CB">{{ item.rightText }}</text>
          <image v-if="item.rightIcon" class="h2.5" mode="heightFix" :src="item.rightIcon" />
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
