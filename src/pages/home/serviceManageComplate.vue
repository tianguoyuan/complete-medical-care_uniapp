<script lang="ts" setup>
import type { ServiceManageSubmitButtonFlag } from './serviceManageInfo.vue'
import type { SignListItem } from '@/components/SignList.vue'
import type { SuccessFailConfig } from '@/components/SuccessFail.vue'

import SuccessFail from '@/components/SuccessFail.vue'
import { PageEnum } from '@/enums/PageEnum'
defineOptions({
  inheritAttrs: false,
})

const query = ref<{ status: ServiceManageSubmitButtonFlag }>()
onLoad((options) => {
  if (options && options.status) {
    query.value = {
      status: options.status as ServiceManageSubmitButtonFlag,
    }
  }
})

const alertConfig = computed<SuccessFailConfig>(() => {
  switch (query.value?.status) {
    case 'rejected':
      return {
        cancelText: '返回首页',
        confirmText: '查看服务详情',
        content: ['您已驳回了该居民的服务申请，', ' 驳回原因：本周临时工作变动不能安排上门服务'],
        subtitle: '审核不通过',
        title: '审核驳回',
        type: 'fail',
      }

    case 'approved':
      return {
        cancelText: '返回首页',
        confirmText: '查看预约详情',
        content: [],
        subtitle: '预约服务申请审核通过',
        title: '审核通过',
        type: 'success',
      }

    case 'cancel':
      return {
        cancelText: '返回首页',
        confirmText: '查看预约详情',
        content: ['您已取消了该居民的服务预约，', ' 取消原因：本周临时工作变动不能安排上门服务'],
        subtitle: '预约服务取消成功',
        title: '取消成功',
        type: 'fail',
      }

    default:
      return {
        cancelText: '',
        confirmText: '',
        content: [],
        subtitle: '',
        title: '',
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
    navigationBarTitleText: '服务结果',
  },
}
</route>
