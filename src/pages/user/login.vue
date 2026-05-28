<script lang="ts" setup>
import type { FormRules, TnFormInstance } from '@tuniao/tnui-vue3-uniapp'

import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'
import TnCheckbox from '@tuniao/tnui-vue3-uniapp/components/checkbox/src/checkbox.vue'
import TnFormItem from '@tuniao/tnui-vue3-uniapp/components/form/src/form-item.vue'
import TnForm from '@tuniao/tnui-vue3-uniapp/components/form/src/form.vue'
import TnInput from '@tuniao/tnui-vue3-uniapp/components/input/src/input.vue'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'

import { PageEnum } from '@/enums/PageEnum'
import { useUserStore } from '@/store'
import { getImage } from '@/utils/imageManager'

const { navBarInfo } = useUniAppSystemRectInfo()
console.log('navBarInfo', navBarInfo)

const userStore = useUserStore()

const formRules: FormRules = {
  agreement: [
    {
      trigger: 'change',
      validator: (rule, value, callback) => {
        if (!value) {
          callback(new Error('请同意协议'))
        }
        callback()
      },
    },
  ],
  password: [
    { message: '请输入密码', required: true, trigger: ['change', 'blur'] },
    {
      message: '请输入6-20位英文、数字、下划线、横线',
      pattern: /^[\w-]{6,20}$/,
      trigger: ['change', 'blur'],
    },
  ],
  username: [
    { message: '请输入用户名', required: true, trigger: ['change', 'blur'] },
    {
      message: '请输入4-16位英文、数字、下划线、横线',
      pattern: /^[\w-]{4,16}$/,
      trigger: ['change', 'blur'],
    },
  ],
}
// 表单数据
const formData = reactive({
  agreement: false,
  password: '',
  username: '',
})

const formRef = ref<TnFormInstance | null>(null)
async function onSubmit() {
  if (!formRef.value) return
  await formRef.value.validate()
  userStore.changeToken(formData.username)
  uni.switchTab({
    url: PageEnum.HOME_PATH,
  })
}
//
</script>

<template>
  <view class="">
    <view class="relative">
      <!-- <view class="absolute bg-#b6e9e5 h-65 w-30 left-0 z-1"></view> -->
      <view class="absolute left-3 z-2" :style="{ marginTop: navBarInfo.height + 30 + 'px' }">
        <view class="text-6">登录</view>
        <view class="mt-1 text-3.5">欢迎使用家医医生端</view>
      </view>

      <image class="w-full" mode="widthFix" :src="getImage('userLoginBg')" />
    </view>
    <view class="relative z-3 mt--6 h-300 rounded-t-6 bg-#fff px-3 py-7.5">
      <TnForm ref="formRef" labelPosition="top" :model="formData" :rules="formRules">
        <TnFormItem label="账号" prop="username">
          <TnInput v-model="formData.username" placeholder="请输入账号" />
        </TnFormItem>

        <TnFormItem label="密码" prop="password">
          <TnInput v-model="formData.password" placeholder="请输入密码" type="password" />
        </TnFormItem>
        <TnFormItem label="" prop="agreement">
          <TnCheckbox v-model="formData.agreement" activeColor="#49B9AD">
            <text class="text-3 color-#1C2023">同意协议</text>
            <text class="text-3 color-#49B9AD">《用户隐私政策》</text>
          </TnCheckbox>
        </TnFormItem>

        <TnFormItem>
          <!-- <tn-button type="primary" @click="onSubmit">登录</tn-button> -->
          <view
            class="mt-7 h-11.25 flex items-center justify-center rounded-2.5 bg-#49B9AD text-3.75 color-#fff"
            @click="onSubmit"
          >
            登录
          </view>
        </TnFormItem>
      </TnForm>
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
    navigationBarTitleText: '登录',
  },
}
</route>
