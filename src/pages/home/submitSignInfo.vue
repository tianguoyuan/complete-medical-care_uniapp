<script lang="ts" setup>
import type { SuccessFailConfig } from '@/components/SuccessFail.vue'

import SuccessFail from '@/components/SuccessFail.vue'
import { PageEnum } from '@/enums/PageEnum'

const successFailConfig: SuccessFailConfig = {
  cancelText: '返回首页',
  confirmText: '查看签约进度',
  content: ['签约信息已提交，居民支付后可完成签约', '签约信息已提交，居民支付后可完成签约'],
  subtitle: '提交成功，等待居民支付',
  title: '提交成功',
  type: 'success',
}

function handleCancel() {
  uni.reLaunch({
    url: PageEnum.HOME_PATH,
  })
}
function handleConfirm() {
  uni.navigateTo({
    url: '/pages/home/pendingSignInfo',
  })
}
</script>

<template>
  <view class="">
    <SuccessFail v-bind="successFailConfig" @cancel="handleCancel" @confirm="handleConfirm" />
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
    navigationBarTitleText: '提交签约信息',
  },
}
</route>
