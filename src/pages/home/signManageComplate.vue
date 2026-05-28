<script lang="ts" setup>
import type { SignListItem } from '@/components/SignList.vue'
import type { SuccessFailConfig } from '@/components/SuccessFail.vue'

import SuccessFail from '@/components/SuccessFail.vue'
import { PageEnum } from '@/enums/PageEnum'
defineOptions({
  inheritAttrs: false,
})

const query = ref<{ status: SignListItem['status'] }>()
onLoad((options) => {
  if (options && options.status) {
    query.value = {
      status: options.status as SignListItem['status'],
    }
  }
})

const alertConfig = computed<SuccessFailConfig>(() => {
  switch (query.value?.status) {
    case 'rejected':
      return {
        cancelText: '返回首页',
        confirmText: '查看签约详情',
        content: [
          '您已驳回了该居民的签约申请，',
          '原因：服务包不适用您的当前年龄，请重新选择后提交',
        ],
        subtitle: '签约失败',
        title: '签约失败',
        type: 'fail',
      }
    case 'pendingPayment':
      return {
        cancelText: '返回首页',
        confirmText: '查看签约详情',
        content: ['您已通过该居民的签约申请，居民支付后可完成签约'],
        subtitle: '签约申请审核通过，等待居民支付',
        title: '签约成功',
        type: 'success',
      }
    default:
      return {
        cancelText: '取消',
        confirmText: '确定',
        content: ['签约成功！'],
        subtitle: '恭喜您，签约成功！',
        title: '签约成功',
        type: 'success',
      }
  }
})
function handleCancel() {
  uni.reLaunch({
    url: PageEnum.HOME_PATH,
  })
}
function handleConfirm() {
  uni.navigateBack()
}
//
</script>

<template>
  <SuccessFail v-bind="alertConfig" @cancel="handleCancel" @confirm="handleConfirm" />
</template>

<style lang="scss" scoped>
//
</style>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '签约结果',
  },
}
</route>
