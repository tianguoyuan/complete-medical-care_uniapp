<script lang="ts" setup>
import type { SignListItem } from '@/components/SignList.vue'

import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import SignList from '@/components/SignList.vue'
import Tabbar from '@/components/Tabbar.vue'
import { PageEnum } from '@/enums/PageEnum'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'
import PLATFORM from '@/utils/platform'
//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const { navBarInfo } = useUniAppSystemRectInfo()
const { systemScreenHeight } = useAppStore()

const countList = ref([
  { content: '1000', title: '已签约人数' },
  { content: '2000', title: '签约指标' },
  { content: '50%', title: '签约率' },
  { content: '2500', title: '服务次数' },
  { content: '3224', title: '服务人数' },
  { content: '80.3%', title: '好评率' },
])

const createList = ref([
  { icon: getImage('homeCreate1'), title: '新建档案', type: 'createUserFile' },
  { icon: getImage('homeCreate2'), title: '签约管理', type: 'signManage' },
  { icon: getImage('homeCreate3'), title: '服务管理', type: 'serviceManage' },
] as const)

const listData = ref<
  {
    count: string
    title: string
    list: SignListItem[]
    type: 'signManage' | 'serviceManage'
  }[]
>([
  {
    count: '2',
    list: [
      {
        age: '58岁',
        keys: [
          { name: '身份证', value: '442355******2225844' },
          { name: '签约团队', value: '阳兰广团队' },
          { name: '服务包', value: '老年人服务包' },
        ],
        name: '韦栋',
        sex: '1',
        status: 'pendingReview',
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
        status: 'pendingReview',
        statusText: '待审核',
      },
    ],
    title: '申请签约',
    type: 'signManage',
  },
  {
    count: '3',
    list: [
      {
        age: '58岁',
        keys: [
          { name: '服务包', value: '老年人服务包' },
          { name: '服务项目', value: '高血压健康随访' },
          { name: '申请时间', value: '2022-09-25 10:00:30' },
        ],
        name: '韦栋',
        sex: '1',
        status: 'pendingReview',
        statusText: '待审核',
      },
    ],
    title: '服务申请',
    type: 'serviceManage',
  },
])

function pageTo(item: (typeof createList.value)[number]) {
  if (item.type === 'createUserFile') {
    uni.navigateTo({
      url: '/pages/home/createUserFile',
    })
  } else if (item.type === 'signManage') {
    uni.navigateTo({
      url: '/pages/home/signManage',
    })
  } else if (item.type === 'serviceManage') {
    uni.navigateTo({
      url: '/pages/home/serviceManage',
    })
  }
}

function handleListClick(item: SignListItem) {
  uni.navigateTo({
    url: `/pages/home/signManageInfo?name=${item.name}&status=${item.status}`,
  })
}

function handleLookAll(type: 'signManage' | 'serviceManage') {
  uni.navigateTo({
    url: `/pages/home/${type}`,
  })
}
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: systemScreenHeight - 50 + 'px' }">
    <view class="bg-[linear-gradient(180deg,#E1FAF7_0.57%,#FFFFFF_100%)]">
      <view :style="{ height: navBarInfo.height + 'px' }"></view>

      <view class="flex items-center justify-between px-3">
        <view class="flex items-center">
          <view class="border-2px border-#fff rounded-full border-solid">
            <image class="h-10 w-10" :src="getImage('mineAvatar')" />
          </view>
          <view class="ml-2.5 text-4">阳兰广医生</view>
        </view>
        <image class="h-5 w-5" :src="getImage('mineQrcode')" />
      </view>

      <view class="mx-3 mt-5">
        <view class="relative grid grid-cols-3 gap-5 rounded-1.5 bg-#49B9AD py-5">
          <view class="absolute left-2.5 top--1 h-5 w-5 rotate-45 rounded-1 bg-#49B9AD"></view>

          <view v-for="(item, index) in countList" :key="index" class="flex flex-col items-center">
            <view class="text-6.25 color-#fff">{{ item.content }}</view>
            <view class="text-2.5 color-#fff">{{ item.title }}</view>
          </view>
        </view>

        <view class="grid grid-cols-3 py-3.75">
          <view
            v-for="(item, index) in createList"
            :key="index"
            class="flex flex-col items-center"
            @click="pageTo(item)"
          >
            <image class="h-12.5 w-12.5" :src="item.icon" />
            <view class="text-2.5 text-3.5 color-#1C2023">{{ item.title }}</view>
          </view>
        </view>
      </view>
    </view>
    <view v-for="(pItem, pIndex) in listData" :key="pIndex">
      <view class="mt-2.5 bg-#fff p-3">
        <view class="flex justify-between">
          <view class="flex items-center">
            <view class="text-4">{{ pItem.title }}</view>
            <view
              class="ml-1 h-3.75 w-3.75 flex items-center justify-center rounded-1.25 rounded-bl-0 bg-#49B9AD color-#fff"
            >
              {{ pItem.count }}
            </view>
          </view>
          <view class="text-3" @click="handleLookAll(pItem.type)">查看全部</view>
        </view>

        <SignList :list="pItem.list" @click="handleListClick" />
      </view>
    </view>

    <Tabbar :tabbarPath="PageEnum.HOME_PATH" />
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '首页',
  },
  needLogin: false,
}
</route>
