<script lang="ts" setup>
import type { SignListItem } from '@/components/SignList.vue'

import TnSticky from '@tuniao/tnui-vue3-uniapp/components/sticky/src/sticky.vue'
import TnTabsItem from '@tuniao/tnui-vue3-uniapp/components/tabs/src/tabs-item.vue'
import TnTabs from '@tuniao/tnui-vue3-uniapp/components/tabs/src/tabs.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import Navbar from '@/components/Navbar.vue'
import SignList from '@/components/SignList.vue'
import { StyleEnum } from '@/enums/StyleEnum'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'
const appStore = useAppStore()

const { navBarInfo } = useUniAppSystemRectInfo()
const currentTabIndex = ref(0)
const tabsList = ref([
  { title: '全部', value: 'all' },
  { title: '待审核', value: 'serviceManagePendingReview' },
  { title: '待服务', value: 'serviceManagePendingService' },
  { title: '已完成', value: 'serviceManageComplete' },
])

const listData = ref<SignListItem[]>([
  {
    age: '58岁',
    keys: [
      { name: '服务包', value: '老年人服务包' },
      { name: '服务项目', value: '高血压健康随访' },
      { name: '申请时间', value: '2022-09-25 10:00:30' },
    ],
    name: '生香海',
    serviceOrg: '机构门诊',
    sex: '1',
    status: 'serviceManagePendingReview',
    statusText: '待审核',
  },

  {
    age: '30岁',
    keys: [
      { name: '服务包', value: '全年免费健康咨询包' },
      { name: '服务项目', value: '健康体验' },
      { name: '申请时间', value: '2022-02-20 12:23:20' },
    ],
    name: '续怡思',
    serviceOrg: '机构门诊',
    sex: '1',
    status: 'serviceManagePendingService',
    statusText: '待服务',
  },

  {
    age: '23岁',
    keys: [
      { name: '服务包', value: '健身体验包' },
      { name: '服务项目', value: '健身体验' },
      { name: '申请时间', value: '2022-01-25 02:55:23' },
    ],
    name: '韦友锦',
    serviceOrg: '机构门诊',
    sex: '1',
    status: 'serviceManageComplete',
    statusText: '已完成',
  },
])

const filterListData = computed(() => {
  const currentTab = tabsList.value[currentTabIndex.value]
  if (!currentTab) return listData.value
  if (currentTab.value === 'all') return listData.value
  return listData.value.filter((item) => item.status === currentTab.value)
})

function handleSignItemClick() {}
//
</script>

<template>
  <view
    class=""
    :style="{
      minHeight: appStore.systemScreenHeight + 'px',
      backgroundColor: '#F5F7FB',
    }"
  >
    <Navbar :bottomShadow="false" fixed showBackIcon showHomeIcon title="服务管理" />

    <TnSticky :offsetTop="+StyleEnum.NAV_BAR_HEIGHT_PX + navBarInfo.statusHeight">
      <TnTabs v-model="currentTabIndex" bgColor="#fff" height="40px" :scroll="false">
        <TnTabsItem v-for="(item, index) in tabsList" :key="index" :title="item.title" />
      </TnTabs>
    </TnSticky>

    <view class="bg-#fff px-3">
      <SignList :list="filterListData" @click="handleSignItemClick" />
    </view>

    <view class="mt-3.75 flex flex-col items-center justify-center">
      <image class="h-7.5 w-7.5" :src="getImage('commonEmpty')" />
      <view class="mt-1.75 color-#C5C8CB">糟糕，到底了</view>
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
    navigationBarTitleText: '服务管理',
  },
}
</route>
