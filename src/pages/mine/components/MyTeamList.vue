<script lang="ts" setup>
export interface ListDataItem {
  img: string
  org: string
  orgId: string
  title: string
}
const props = defineProps<{
  listData: ListDataItem[]
}>()
</script>

<template>
  <view v-for="item in props.listData" :key="item.orgId" class="flex px-3 pb-3.75">
    <view>
      <image class="h-22.5 w-22.5 rounded-2" :src="item.img" />
    </view>
    <view class="ml-5">
      <view class="text-4 line-height-5.75">{{ item.title }}</view>
      <view class="mt-1.25 text-3 color-#606972">
        <text>所属机构:</text>
        <text class="pl-1.25">{{ item.org }}</text>
      </view>

      <view class="mt-1.25 text-3 color-#606972">
        <text>团队编号:</text>
        <text class="pl-1.25">{{ item.orgId }}</text>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>
