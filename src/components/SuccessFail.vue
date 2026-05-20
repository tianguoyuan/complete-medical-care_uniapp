<script lang="ts" setup>
//
import Navbar from '@/components/Navbar.vue'
import { getImage } from '@/utils/imageManager'
export interface SuccessFailConfig {
  cancelText: string
  confirmText: string
  content: string[]
  subtitle: string
  title: string
  type: 'success' | 'fail'
}

const props = defineProps<SuccessFailConfig>()
</script>

<template>
  <view class="">
    <Navbar fixed show-back-icon show-home-icon :title="props.title" />

    <view class="mt-14">
      <image
        class="h-43.75 w-43.75"
        :src="getImage(props.type === 'success' ? 'commonSuccess' : 'commonFail')"
      />

      <view class="text-center">
        <view class="mt-5 text-4">{{ props.subtitle }}</view>
        <view v-for="(item, index) in props.content" :key="index" class="mt-2.5 color-#606972">
          {{ item }}
        </view>
      </view>

      <view class="mx-3 mt-8.75">
        <view class="h-10 rounded-2.5 bg-#49B9AD color-#fff">{{ props.confirmText }}</view>
        <view class="mt-3.75 h-10 border border-#49B9AD rounded-2.5 border-solid color-#49B9AD">
          {{ props.cancelText }}
        </view>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
//
</style>
