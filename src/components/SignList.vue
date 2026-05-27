<script lang="ts" setup>
import { getImage } from '@/utils/imageManager'

// {
//   age: '58岁',
//   keys: [
//     { name: '身份证', value: '442355******2225844' },
//     { name: '签约团队', value: '阳兰广团队' },
//     { name: '服务包', value: '老年人服务包' },
//   ],
//   name: '韦栋',
//   sex: '1',
//   status: 'pending',
//   statusText: '待审核',
// },
// { title: '待审核', value: 'pendingReview' },
// { title: '待支付', value: 'pendingPayment' },
// { title: '已签约', value: 'signed' },
// { title: '已驳回', value: 'rejected' },

export interface SignListItem {
  age: string
  keys: { name: string; value: string }[]
  name: string
  sex: string
  status: 'pendingReview' | 'pendingPayment' | 'signed' | 'rejected'
  statusText: '待审核' | '待支付' | '已签约' | '已驳回'
}
const props = defineProps<{
  list: SignListItem[]
}>()
//
</script>

<template>
  <view
    v-for="(item, index) in props.list"
    :key="index"
    class="mt-3.75 flex flex-col border-0 border-#E3E4E5 border-solid"
    :class="props.list.length - 1 === index ? 'pb-0 border-0' : 'pb-3.5 border-b-1'"
  >
    <view class="flex items-center justify-between">
      <view class="flex items-center">
        <image class="h-5 w-5" :src="getImage(item.sex === '1' ? 'commonBoy' : 'commonGirl')" />

        <view class="ml-2.5">
          <view class="flex items-end">
            <view class="text-3.75">{{ item.name }}</view>
            <view class="ml-1.25">{{ item.age }}</view>
          </view>
        </view>
      </view>
      <view
        class="h-5 w-12.5 flex items-center justify-center rounded-2.5 bg-#FFF2E8 color-#FA541C"
      >
        {{ item.statusText }}
      </view>
    </view>
    <view v-for="(kItem, kIndex) in item.keys" :key="kIndex" class="mt-2.5 flex">
      <view class="ml-7.5 w-17.5 text-3.5 text-3.75">{{ kItem.name }}</view>
      <view class="ml-1.25">{{ kItem.value }}</view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>
