<script lang="ts" setup>
import type { SignListItem } from '@/components/SignList.vue'

import TnSticky from '@tuniao/tnui-vue3-uniapp/components/sticky/src/sticky.vue'
import TnTabsItem from '@tuniao/tnui-vue3-uniapp/components/tabs/src/tabs-item.vue'
import TnTabs from '@tuniao/tnui-vue3-uniapp/components/tabs/src/tabs.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import Navbar from '@/components/Navbar.vue'
import SignList from '@/components/SignList.vue'
import { StyleEnum } from '@/enums/StyleEnum'

const { navBarInfo } = useUniAppSystemRectInfo()
const currentTabIndex = ref(0)
const tabsList = ref([
  { title: '全部', value: 'all' },
  { title: '待审核', value: 'pendingReview' },
  { title: '待支付', value: 'pendingPayment' },
  { title: '已签约', value: 'signed' },
  { title: '已驳回', value: 'rejected' },
])

const listData = ref<SignListItem[]>([
  {
    age: '58岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '老年人服务包' },
    ],
    name: '官兰伟',
    sex: '1',
    status: 'pendingReview',
    statusText: '待审核',
  },
  {
    age: '29岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '妇女保健包' },
    ],
    name: '凤珠德',
    sex: '0',
    status: 'rejected',
    statusText: '已驳回',
  },
  {
    age: '23岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '健康体验包' },
    ],
    name: '明兰',
    sex: '0',
    status: 'signed',
    statusText: '已签约',
  },
  {
    age: '10岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '幼儿年度体检包' },
    ],
    name: '思蓝',
    sex: '0',
    status: 'pendingPayment',
    statusText: '待支付',
  },
  {
    age: '58岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '老年人服务包' },
    ],
    name: '刘思浩',
    sex: '1',
    status: 'pendingReview',
    statusText: '待审核',
  },

  {
    age: '10岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '幼儿年度体检包' },
    ],
    name: '思蓝',
    sex: '0',
    status: 'pendingPayment',
    statusText: '待支付',
  },
  {
    age: '58岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '老年人服务包' },
    ],
    name: '刘思浩',
    sex: '1',
    status: 'pendingReview',
    statusText: '待审核',
  },

  {
    age: '10岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '幼儿年度体检包' },
    ],
    name: '思蓝',
    sex: '0',
    status: 'pendingPayment',
    statusText: '待支付',
  },
  {
    age: '58岁',
    keys: [
      { name: '身份证', value: '442355******2225844' },
      { name: '签约团队', value: '阳兰广团队' },
      { name: '服务包', value: '老年人服务包' },
    ],
    name: '刘思浩',
    sex: '1',
    status: 'pendingReview',
    statusText: '待审核',
  },
])

const filterListData = computed(() => {
  const currentTab = tabsList.value[currentTabIndex.value]
  if (!currentTab) return listData.value
  if (currentTab.value === 'all') return listData.value
  return listData.value.filter((item) => item.status === currentTab.value)
})

function handleSignItemClick(value: SignListItem, index: number) {
  console.log('点击了签约项：', value, index)
  if (value.status === 'signed') {
    uni.navigateTo({
      url: `/pages/home/signManageComplate?status=${value.status}&name=${value.name}`,
    })
  } else {
    uni.navigateTo({
      url: `/pages/home/signManageInfo?status=${value.status}&name=${value.name}`,
    })
  }
}

//
</script>

<template>
  <view class="">
    <Navbar :bottomShadow="false" fixed showBackIcon showHomeIcon title="签约管理" />
    <TnSticky :offsetTop="+StyleEnum.NAV_BAR_HEIGHT_PX + navBarInfo.statusHeight">
      <TnTabs v-model="currentTabIndex" bgColor="#fff" height="40px" :scroll="false">
        <TnTabsItem v-for="(item, index) in tabsList" :key="index" :title="item.title" />
      </TnTabs>
    </TnSticky>

    <view class="px-3"><SignList :list="filterListData" @click="handleSignItemClick" /></view>

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
    navigationBarTitleText: '签约管理',
  },
}
</route>
