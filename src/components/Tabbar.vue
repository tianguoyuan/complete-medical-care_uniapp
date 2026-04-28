<script lang="ts" setup>
import TnTabbar from '@tuniao/tnui-vue3-uniapp/components/tabbar/src/tabbar.vue'
import TnTabbarItem from '@tuniao/tnui-vue3-uniapp/components/tabbar/src/tabbar-item.vue'
import { useTabbarStore } from '@/store/tabbar'
import { getImage } from '@/utils/imageManager'
import PLATFORM from '@/utils/platform'
import { StyleEnum } from '@/enums/StyleEnum'

const tabbarStore = useTabbarStore()

const tabbarList = [
  {
    title: '首页',
    icon: getImage('home'),
    activeIcon: getImage('homeActive'),
    path: '/pages/home/home',
  },
  {
    title: '居民',
    icon: getImage('resident'),
    activeIcon: getImage('residentActive'),
    path: '/pages/resident/resident',
  },
  {
    title: '消息',
    icon: getImage('message'),
    activeIcon: getImage('messageActive'),
    path: '/pages/message/message',
  },
  {
    title: '我的',
    icon: getImage('mine'),
    activeIcon: getImage('mineActive'),
    path: '/pages/mine/mine',
  },
] as const
type PathType = (typeof tabbarList)[number]['path']
const props = withDefaults(
  defineProps<{
    tabbarPath: PathType
    topShadow: boolean
  }>(),
  {
    topShadow: true,
  },
)

// 初次进入生效
const tabbarIndex = tabbarList.findIndex((v) => v.path === props.tabbarPath)
tabbarStore.changeTabbarIndex(tabbarIndex)

function pageTo(index: number) {
  tabbarStore.changeTabbarIndex(index)
  const path = tabbarList[index]?.path
  if (!path) return
  uni.switchTab({ url: path })
}
</script>

<template>
  <!-- h5多一个占位tabbar高度, 其它没有 -->
  <view v-if="!PLATFORM.isH5" class="h-12.5" />
  <TnTabbar
    v-if="!tabbarStore.hideTabbar"
    :model-value="tabbarStore.tabbarIndex"
    fixed
    :bg-color="StyleEnum.MAIN_COLOR"
    safe-area-inset-bottom
    :top-shadow="props.topShadow"
    placeholder
    height="100rpx"
  >
    <TnTabbarItem v-for="(item, index) in tabbarList" :key="index" @click="pageTo(index)">
      <template #default>
        <view v-if="item.title" class="h-100rpx flex-1 flex items-center justify-center">
          <view class="flex flex-col items-center justify-center text-3">
            <view>
              <image
                v-show="index === tabbarStore.tabbarIndex"
                :src="item.activeIcon"
                class="w-5 h-5"
              />
              <image v-show="index !== tabbarStore.tabbarIndex" :src="item.icon" class="w-5 h-5" />
            </view>
            <view
              class="mt-1"
              :class="[index === tabbarStore.tabbarIndex ? 'text-[#49b9ad]' : 'text-[#1c2023]']"
            >
              {{ item.title }}
            </view>
          </view>
        </view>

        <view v-else class="flex-1 flex items-start">
          <image :src="(item as (typeof tabbarList)[0]).icon" class="w-9 h-9 mt-1" />
        </view>
      </template>
    </TnTabbarItem>
  </TnTabbar>
</template>

<style lang="scss">
//
</style>
