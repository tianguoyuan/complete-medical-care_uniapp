<script lang="ts" setup>
import PLATFORM from '@/utils/platform'
import Tabbar from '@/components/Tabbar.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'
import { getImage } from '@/utils/imageManager'
import { useAppStore } from '@/store/app'
//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const { navBarInfo } = useUniAppSystemRectInfo()
const { systemScreenHeight } = useAppStore()

const countList = ref([
  { title: '已签约人数', content: '1000' },
  { title: '签约指标', content: '2000' },
  { title: '签约率', content: '50%' },
  { title: '服务次数', content: '2500' },
  { title: '服务人数', content: '3224' },
  { title: '好评率', content: '80.3%' },
])

const createList = ref([
  { type: 'create', title: '新建档案', icon: getImage('homeCreate1') },
  { type: 'signContract', title: '签约管理', icon: getImage('homeCreate2') },
  { type: 'service', title: '服务管理', icon: getImage('homeCreate3') },
] as const)

const listData = ref([
  {
    title: '申请签约',
    count: '2',
    list: [
      {
        name: '韦栋',
        age: '58岁',
        sex: '1',
        status: 'pending',
        statusText: '待审核',
        keys: [
          { name: '身份证', value: '442355******2225844' },
          { name: '签约团队', value: '阳兰广团队' },
          { name: '服务包', value: '老年人服务包' },
        ],
      },

      {
        name: '化姣',
        age: '29岁',
        sex: '0',
        status: 'pending',
        statusText: '待审核',
        keys: [
          { name: '身份证', value: '440682******9875624' },
          { name: '签约团队', value: '阳兰广团队' },
          { name: '服务包', value: '妇女保健包' },
        ],
      },
    ],
  },
  {
    title: '服务申请',
    count: '3',
    list: [
      {
        name: '韦栋',
        age: '58岁',
        sex: '1',
        status: 'pending',
        statusText: '待审核',
        keys: [
          { name: '服务包', value: '老年人服务包' },
          { name: '服务项目', value: '高血压健康随访' },
          { name: '申请时间', value: '2022-09-25 10:00:30' },
        ],
      },
    ],
  },
])

function pageTo(item: (typeof createList.value)[number]) {
  if (item.type === 'create') {
    uni.navigateTo({
      url: '/pages/home/createUserFile',
    })
  }
}
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: systemScreenHeight - 50 + 'px' }">
    <view class="bg-[linear-gradient(180deg,#E1FAF7_0.57%,#FFFFFF_100%)]">
      <view :style="{ height: navBarInfo.height + 'px' }"></view>

      <view class="flex justify-between items-center px-3">
        <view class="flex items-center">
          <view class="rounded-full border-2px border-solid border-#fff">
            <image :src="getImage('mineAvatar')" class="w-10 h-10" />
          </view>
          <view class="ml-2.5 text-4">阳兰广医生</view>
        </view>
        <image :src="getImage('mineQrcode')" class="w-5 h-5" />
      </view>

      <view class="mt-5 mx-3">
        <view class="bg-#49B9AD rounded-1.5 grid grid-cols-3 gap-5 py-5 relative">
          <view class="bg-#49B9AD w-5 h-5 rounded-1 rotate-45 absolute top--1 left-2.5"></view>

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
            <image :src="item.icon" class="w-12.5 h-12.5" />
            <view class="text-2.5 color-#1C2023 text-3.5">{{ item.title }}</view>
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
              class="bg-#49B9AD rounded-1.25 color-#fff rounded-bl-0 w-3.75 h-3.75 flex justify-center items-center ml-1"
            >
              {{ pItem.count }}
            </view>
          </view>
          <view class="text-3">查看全部</view>
        </view>

        <view
          class="mt-3.75 flex flex-col border-0 border-solid border-#E3E4E5"
          v-for="(item, index) in pItem.list"
          :key="index"
          :class="pItem.list.length - 1 === index ? 'pb-0 border-0' : 'pb-3.5 border-b-1'"
        >
          <view class="flex justify-between items-center">
            <view class="flex items-center">
              <image
                :src="getImage(item.sex === '1' ? 'commonBoy' : 'commonGirl')"
                class="w-5 h-5"
              />

              <view class="ml-2.5">
                <view class="flex items-end">
                  <view class="text-3.75">{{ item.name }}</view>
                  <view class="ml-1.25">{{ item.age }}</view>
                </view>
              </view>
            </view>
            <view
              class="w-12.5 h-5 bg-#FFF2E8 color-#FA541C rounded-2.5 flex items-center justify-center"
            >
              {{ item.statusText }}
            </view>
          </view>
          <view v-for="(kItem, kIndex) in item.keys" :key="kIndex" class="flex mt-2.5">
            <view class="text-3.75 ml-7.5 text-3.5 w-17.5">{{ kItem.name }}</view>
            <view class="ml-1.25">{{ kItem.value }}</view>
          </view>
        </view>
      </view>
    </view>

    <Tabbar tabbar-path="/pages/home/home" />
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
