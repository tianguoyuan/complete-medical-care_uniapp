<script lang="ts" setup>
import Navbar from '@/components/Navbar.vue'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'

import MyTeamList, { type ListDataItem } from './components/MyTeamList.vue'

const appStore = useAppStore()

const listDataManagement = ref<ListDataItem[]>([
  {
    img: getImage('mineMyTeamList1'),
    org: '佛山市桂雅社区卫生服务站',
    orgId: '0234581',
    title: '李晓丽专科团队',
  },
  {
    img: getImage('mineMyTeamList2'),
    org: '佛山市桂雅社区卫生服务站',
    orgId: '0234853',
    title: '阳兰广团队',
  },
])
const listDataJoin = ref<ListDataItem[]>([
  {
    img: getImage('mineMyTeamList3'),
    org: '佛山市桂雅社区卫生服务站',
    orgId: '0234581',
    title: '李晓丽专科团队',
  },
  {
    img: getImage('mineMyTeamList4'),
    org: '佛山市奇槎社区卫生服务站',
    orgId: '0232544',
    title: '潘晓婷团队',
  },
  {
    img: getImage('mineMyTeamList4'),
    org: '佛山市奇槎社区卫生服务站',
    orgId: '0232544',
    title: '潘晓婷团队',
  },
])
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: appStore.systemScreenHeight + 'px' }">
    <Navbar fixed showBackIcon showHomeIcon title="我的团队" />

    <view class="bg-#fff pt-2.5">
      <view class="ml-3 mt-2.5 pb-3.5 text-4 line-height-5.75">我管理的团队</view>
      <MyTeamList :listData="listDataManagement" />
    </view>

    <view class="mt-2.5 bg-#fff pt-2.5">
      <view class="ml-3 mt-2.5 pb-3.5 text-4 line-height-5.75">我加入的团队</view>
      <MyTeamList :listData="listDataJoin" />
    </view>

    <view class="h-22 pb-safe"></view>
    <view
      class="fixed bottom-0 left-0 right-0 border-0 border-t border-#E3E4E5 border-solid bg-#fff pb-safe"
    >
      <view class="px-3 py-1.25">
        <view
          class="h-10 flex items-center justify-center rounded-2.5 bg-#49B9AD text-3.75 color-#fff"
        >
          加入团队
        </view>
      </view>

      <view class="h-8.5"></view>
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
    navigationBarTitleText: '我的团队',
  },
}
</route>
