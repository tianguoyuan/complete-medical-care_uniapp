<script lang="ts" setup>
import type { ListDataItem } from '@/components/UserTagList.vue'

import { TnInput } from '@tuniao/tnui-vue3-uniapp'

import Tabbar from '@/components/Tabbar.vue'
import UserTagList from '@/components/UserTagList.vue'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'
import PLATFORM from '@/utils/platform'

//
onLoad(() => PLATFORM.isApp && uni.hideTabBar())

const appStore = useAppStore()

const tagList = [
  {
    icon: getImage('residentTag1'),
    path: '',
    title: '未签约居民',
  },
  {
    icon: getImage('residentTag2'),
    path: '/pages/resident/tag',
    title: '标签',
  },
  {
    icon: getImage('residentTag3'),
    path: '/pages/resident/message',
    title: '群发信息',
  },
]

const userList = [
  {
    sort: 'A',
    userList: [
      {
        age: '12岁',
        name: '安娅志',
        sex: 'female',
        tagList: [
          {
            bgc: '#EAFEFA',
            color: '#49B9AD',
            title: '发育不良',
          },
          {
            bgc: '#FFF2E8',
            color: '#FA541C',
            title: '贫血',
          },
        ],
      },
      {
        age: '42岁',
        name: '啊玲',
        sex: 'female',
        tagList: [
          {
            bgc: '#EAFEFA',
            color: '#49B9AD',
            title: '乳腺结节',
          },
          {
            bgc: '#FFF2E8',
            color: '#FA541C',
            title: '贫血',
          },
        ],
      },
    ],
  },

  {
    sort: 'B',
    userList: [
      {
        age: '30岁',
        name: '包文星',
        sex: 'male',
        tagList: [
          {
            bgc: '#EAFEFA',
            color: '#49B9AD',
            title: '高血脂',
          },
        ],
      },
      {
        age: '42岁',
        name: '布李嘉玲',
        sex: 'female',
        tagList: [
          {
            bgc: '#FFF2E8',
            color: '#FA541C',
            title: '贫血',
          },
        ],
      },
    ],
  },
]

function handleClickTag(path: string) {
  if (!path) return
  uni.navigateTo({
    url: path,
  })
}
function tagClick(tag: ListDataItem) {
  uni.navigateTo({
    url: `/pages/home/signManageInfo?name=${tag.name}`,
  })
}
</script>

<template>
  <view class="bg-#F5F7FB" :style="{ minHeight: appStore.systemScreenHeight + 'px' }">
    <view class="bg-#fff">
      <view class="px-3">
        <view class="z-10 h-10 flex items-center rounded-2.5 bg-#F5F7FB px-3.75">
          <image class="h-5 w-5" :src="getImage('commonSearch')" />
          <TnInput :border="false" height="40" placeholder="搜索居民姓名/电话" />
        </view>
      </view>

      <view class="pb-3.75">
        <view
          v-for="(item, index) in tagList"
          :key="index"
          class="ml-3 mt-5 flex items-center"
          @click="handleClickTag(item.path)"
        >
          <image class="h-10 w-10" :src="item.icon" />
          <view class="ml-4 text-3.75">{{ item.title }}</view>
        </view>
      </view>

      <view>
        <view v-for="(item, index) in userList" :key="index">
          <view class="h-9 bg-#F5F7FB pl-3.25 pt-3.75">{{ item.sort }}</view>
          <UserTagList :listData="item.userList" @tag-click="tagClick" />
        </view>
      </view>
    </view>

    <Tabbar tabbarPath="/pages/resident/resident" />
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'default',
    navigationBarTitleText: '居民',
  },
  needLogin: false,
}
</route>
