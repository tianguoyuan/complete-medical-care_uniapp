<script lang="ts" setup>
import type { SignListItem } from '@/components/SignList.vue'

import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp'

import Navbar from '@/components/Navbar.vue'
import SignList from '@/components/SignList.vue'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'

const { systemScreenHeight } = useAppStore()

const listData = ref<SignListItem[]>([
  {
    age: '58岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '老年人服务包' },
    ],
    name: '韦栋',
    sex: '1',
    status: 'pending',
    statusText: '待审核',
  },

  {
    age: '29岁',
    keys: [
      { name: '身份证', value: '440682******9875624' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '妇女保健包' },
    ],
    name: '化姣',
    sex: '0',
    status: 'pending',
    statusText: '待审核',
  },
])
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: systemScreenHeight + 'px' }">
    <Navbar fixed show-back-icon show-home-icon title="待处理签约申请" />
    <view class="bg-#fff px-3 py-3.75">
      <SignList :list="listData" />
    </view>

    <view class="mt-3.75 flex flex-col items-center justify-center">
      <image class="h-7.5 w-7.5" :src="getImage('commonEmpty')" />
      <view class="mt-3.75 color-#C5C8CB">糟糕，到底了</view>
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
    navigationStyle: 'custom',
    navigationBarTitleText: '待处理签约申请',
  },
}
</route>
