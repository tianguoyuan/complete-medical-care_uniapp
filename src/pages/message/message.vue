<script lang="ts" setup>
import Navbar from '@/components/Navbar.vue'
import Tabbar from '@/components/Tabbar.vue'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'
const appStore = useAppStore()

const messageList = ref([
  {
    isRead: false,
    subtitle: '觉得我们好用就给个好评吧～',
    title: '评分提醒',
  },
  {
    isRead: true,
    subtitle: '新版本来啦～',
    title: '版本更新',
  },
])
</script>

<template>
  <view
    class=""
    :style="{ minHeight: appStore.systemScreenHeight + 'px', backgroundColor: '#f5f7fb' }"
  >
    <Navbar title="服务消息" />

    <view class="bg-#fff px-3">
      <view
        v-for="(item, index) in messageList"
        :key="index"
        class="flex items-center justify-between border-0 border-b border-#E3E4E5 border-b-solid px-3 py-3.75"
      >
        <view class="flex-1">
          <view class="flex items-center line-height-5.25">
            <view class="text-3.75">{{ item.title }}</view>
            <view v-if="!item.isRead" class="ml-1.75 h-2.5 w-2.5 rounded-full bg-#F65755"></view>
          </view>
          <view class="mt-0.75 text-3 color-#C5C8CB line-height-4.25">{{ item.subtitle }}</view>
        </view>
        <image class="h-2.5 w-2.5" :src="getImage('commonArrowRight')" />
      </view>
    </view>
    <Tabbar tabbarPath="/pages/message/message" />
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
    navigationBarTitleText: '消息',
  },
}
</route>
