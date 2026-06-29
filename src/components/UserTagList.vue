<script lang="ts" setup>
import { getImage } from '@/utils/imageManager'

//
const props = defineProps<{
  listData: {
    age: string
    name: string
    sex: string
    tagList: {
      bgc: string
      color: string
      title: string
    }[]
  }[]
}>()
</script>

<template>
  <view v-for="(item, index) in props.listData" :key="index" class="">
    <view class="flex items-center px-3 py-4 pb-0">
      <image
        class="h-10 w-10"
        :src="getImage(`common${item.sex === 'male' ? 'Male' : 'Female'}`)"
      />
      <view class="ml-2.5 flex-1">
        <view class="flex items-center line-height-5.25">
          <view class="mr-1.25 text-3.75">{{ item.name }}</view>
          <view class="mr-2 text-3">{{ item.age }}</view>
          <image
            class="h-2.5 w-2.5"
            :src="item.sex === 'male' ? getImage('commonBoy') : getImage('commonGirl')"
          />
        </view>
        <view class="mr-2.5 mt-1.25 flex pr-9">
          <view v-for="(j, k) in item.tagList" :key="k" class="">
            <view
              class="rounded-full px-2.5 text-2.5 text-2.5 line-height-4"
              :style="{
                backgroundColor: j.bgc,
                color: j.color,
                border: `1px solid ${j.color}
          `,
              }"
            >
              {{ j.title }}
            </view>
          </view>
        </view>
      </view>
    </view>
    <view class="h-4"></view>
    <view class="ml-15.5 mr-9 h-1px bg-#E3E4E5"></view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>
