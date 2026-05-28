<script lang="ts" setup>
import type { AlertProps } from '@/components/Alert.vue'
import type { FormItemConfig } from '@/components/FormGenerate.vue'
import type { FormInfoItem } from '@/components/FormInfo.vue'
import type { SignListItem } from '@/components/SignList.vue'

import Alert from '@/components/Alert.vue'
import FormGenerate from '@/components/FormGenerate.vue'
import FormInfo from '@/components/FormInfo.vue'
import Navbar from '@/components/Navbar.vue'
import { useAppStore } from '@/store/app'

const appStore = useAppStore()

const personInfoList = ref<FormInfoItem[]>([
  {
    name: '真实姓名',
    value: '王紫嫣',
  },
  {
    name: '身份证号',
    value: '524895123548752236',
  },
  {
    name: '性别',
    value: '女',
  },
  {
    name: '年龄',
    value: '23',
  },
  {
    name: '联系电话',
    value: '13800138000',
  },
  {
    name: '现居住地',
    value: '南海区常青路58号2栋23楼2356室',
  },
])
const signInfoList = ref<FormInfoItem[]>([
  {
    name: '签约状态',
    value: '待审核',
    valueColor: '#F65755',
  },
  {
    name: '签约机构',
    value: '桂雅卫生服务站',
  },
  {
    name: '签约医生',
    value: '阳兰广',
  },
  {
    name: '服务包',
    value: '健康体验包',
  },
  {
    name: '签约周期',
    value: '2年',
  },
  {
    name: '现居住地',
    value: '南海区常青路58号2栋23楼2356室',
  },
  {
    name: '费用',
    value: '¥200',
    valueColor: '#F65755',
  },
  {
    name: '签约申请时间',
    value: '2022/05/26 10:20:30',
  },
])

interface SignManageInfoPageQuery {
  name: SignListItem['name']
  status: SignListItem['status']
}

defineOptions({
  inheritAttrs: false,
})
const query = ref<SignManageInfoPageQuery>({
  name: '',
  status: 'pendingReview',
})

const alertConfig = computed<AlertProps>(() => {
  switch (query.value.status) {
    case 'pendingReview':
      return {
        icon: 'time-fill',
        title: '等待医生审核中',
        type: 'success',
      }
    case 'pendingPayment':
      return {
        icon: 'paperbag-fill',
        title: '审核通过，等待居民支付中',
        type: 'success',
      }
    case 'signed':
      return {
        icon: 'success-circle-fill',
        title: '签约成功',
        type: 'success',
      }
    case 'rejected':
      return {
        icon: 'close-fill',
        title: '已驳回',
        type: 'error',
      }
    default:
      return {
        icon: 'time-fill',
        title: '',
        type: 'success',
      }
  }
})
onLoad((options) => {
  if (options && options.status && options.name) {
    query.value = {
      name: options.name,
      status: options.status as SignListItem['status'],
    }
  }
})

function handleClick(status: SignListItem['status']) {
  if (status === 'rejected') {
    // 驳回
    uni.navigateTo({
      url: '/pages/home/signManageComplate?status=rejected',
    })
  } else if (status === 'pendingPayment') {
    // 审核通过
    uni.navigateTo({
      url: '/pages/home/signManageComplate?status=pendingPayment',
    })
  }
}
</script>

<template>
  <view
    class="bg-#F5F7FB"
    :style="{
      minHeight: appStore.systemScreenHeight + 'px',
    }"
  >
    <Navbar fixed showBackIcon showHomeIcon title="签约详情" />
    <Alert v-bind="alertConfig" />

    <view class="bg-#fff px-3">
      <view class="text-4 line-height-13">居民信息</view>
      <FormInfo :listData="personInfoList" />
    </view>

    <view class="mt-2.5 bg-#fff px-3">
      <view class="text-4 line-height-13">签约信息</view>
      <FormInfo :listData="signInfoList" />
    </view>

    <view class="mt-2.5 bg-#fff px-3 pb-3.75">
      <view class="text-4 line-height-13">签约备注</view>
      <view class="h-37.5 rounded-2 bg-#F5F7FB p-3.75">无</view>
    </view>

    <view v-if="query.status === 'pendingReview'" class="mt-4.5 bg-#fff py-1 pb-5">
      <view class="mx-5 flex items-center justify-between text-3.75 pb-safe">
        <view
          class="h-10 flex flex-1 items-center justify-center border-1 border-#F65755 rounded-2.5 border-solid color-#F65755"
          @click="handleClick('rejected')"
        >
          驳回
        </view>
        <view
          class="ml-2.5 h-10 flex flex-1 items-center justify-center rounded-2.5 bg-#49B9AD color-#fff"
          @click="handleClick('pendingPayment')"
        >
          审核通过
        </view>
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
    navigationBarTitleText: '签约详情',
  },
}
</route>
