<script lang="ts" setup>
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

const emits = defineEmits<{
  (e: 'cancel'): void
  (e: 'confirm'): void
}>()
</script>

<template>
  <view class="">
    <Navbar
      bgColor="transparent"
      :bottomShadow="false"
      fixed
      showBackIcon
      showHomeIcon
      :title="props.title"
    />
    <view
      class="absolute left-0 right-0 top-0 h-40 blur-2xl"
      :class="[props.type === 'success' ? 'bg-#EAFEFA' : 'bg-#FEF1F1']"
    ></view>

    <view class="mt-14">
      <view class="flex justify-center">
        <image
          class="h-43.75 w-43.75"
          :src="getImage(props.type === 'success' ? 'commonSuccess' : 'commonFail')"
        />
      </view>

      <view class="text-center">
        <view class="mt-5 text-4">{{ props.subtitle }}</view>
        <view class="mt-2.5">
          <view
            v-for="(item, index) in props.content"
            :key="index"
            class="color-#606972 line-height-4"
          >
            {{ item }}
          </view>
        </view>
      </view>

      <view class="mx-3 mt-8.75 text-3.75">
        <view
          class="h-10 flex items-center justify-center rounded-2.5 bg-#49B9AD color-#fff"
          @click="emits('confirm')"
        >
          {{ props.confirmText }}
        </view>
        <view
          class="mt-3.75 h-10 flex items-center justify-center border border-#49B9AD rounded-2.5 border-solid color-#49B9AD"
          @click="emits('cancel')"
        >
          {{ props.cancelText }}
        </view>
      </view>
    </view>
  </view>
</template>
