<script lang="ts" setup>
import { TnInput } from '@tuniao/tnui-vue3-uniapp'

import Navbar from '@/components/Navbar.vue'
import UserTagList from '@/components/UserTagList.vue'
import { useAppStore } from '@/store/app'
import { getImage } from '@/utils/imageManager'

const appStore = useAppStore()

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
function submit() {
  uni.navigateBack()
}
</script>

<template>
  <view
    class=""
    :style="{ minHeight: appStore.systemScreenHeight + 'px', backgroundColor: '#F5F7FB' }"
  >
    <Navbar fixed showBackIcon showHomeIcon title="设置标签">
      <template #right>
        <view class="color-#49B9AD" @click="submit">完成</view>
      </template>
    </Navbar>

    <view class="bg-#fff px-3">
      <view class="pt-3.75 text-3.25 color-#C5C8CB">标签名字</view>
      <view class="mt-2 border-0 border-b border-#E3E4E5 border-solid">
        <TnInput :border="false" placeholder="请输入标签名称" />
      </view>

      <view class="mt-3.75 text-3.25 color-#C5C8CB">标签成员(0)</view>
      <view class="mt-2.25 flex items-center color-#49B9AD">
        <image class="h-3 w-3" :src="getImage('commonAdd')" />
        <view class="ml-1.75">添加居民</view>
      </view>

      <view class="h-4.5"></view>
      <view class="h-1px bg-#E3E4E5"></view>
    </view>

    <view class="bg-#fff">
      <view v-for="(item, index) in userList" :key="index">
        <view class="h-9 bg-#F5F7FB pl-3.25 pt-3.75">{{ item.sort }}</view>
        <UserTagList :listData="item.userList" />
      </view>
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
    navigationBarTitleText: '设置标签',
  },
}
</route>
