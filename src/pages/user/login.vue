<script lang="ts" setup>
import { getImage } from '@/utils/imageManager'
import { useUniAppSystemRectInfo } from '@tuniao/tnui-vue3-uniapp/hooks'
import TnForm from '@tuniao/tnui-vue3-uniapp/components/form/src/form.vue'
import TnFormItem from '@tuniao/tnui-vue3-uniapp/components/form/src/form-item.vue'
import TnCheckbox from '@tuniao/tnui-vue3-uniapp/components/checkbox/src/checkbox.vue'
import TnInput from '@tuniao/tnui-vue3-uniapp/components/input/src/input.vue'
import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'

import type { FormRules, TnFormInstance } from '@tuniao/tnui-vue3-uniapp'

const { navBarInfo } = useUniAppSystemRectInfo()
console.log('navBarInfo', navBarInfo)

const formRules: FormRules = {
  username: [
    { required: true, message: '请输入用户名', trigger: ['change', 'blur'] },
    {
      pattern: /^[\w-]{4,16}$/,
      message: '请输入4-16位英文、数字、下划线、横线',
      trigger: ['change', 'blur'],
    },
  ],
  password: [
    { required: true, message: '请输入密码', trigger: ['change', 'blur'] },
    {
      pattern: /^[\w-]{6,20}$/,
      message: '请输入6-20位英文、数字、下划线、横线',
      trigger: ['change', 'blur'],
    },
  ],
  agreement: [
    {
      validator: (rule, value, callback) => {
        if (!value) {
          callback(new Error('请同意协议'))
        }
        callback()
      },
      trigger: 'change',
    },
  ],
}
// 表单数据
const formData = reactive({
  username: '',
  password: '',
  agreement: false,
})

const formRef = ref<TnFormInstance | null>(null)
function onSubmit() {
  if (!formRef.value) return
  formRef.value.validate((valid: boolean) => {
    if (valid) {
      console.log('表单验证通过，提交数据', formData)
      // 在这里执行登录逻辑，例如调用登录接口
    } else {
      console.log('表单验证失败')
      return false
    }
  })
}
//
</script>

<template>
  <view class="">
    <view class="relative">
      <view class="absolute bg-#b6e9e5 h-60 w-60 translate-x--60% z-1"></view>
      <view class="absolute left-3 z-2" :style="{ marginTop: navBarInfo.height + 30 + 'px' }">
        <view class="text-6">登录</view>
        <view class="mt-1 text-3.5">欢迎使用家医医生端</view>
      </view>

      <image :src="getImage('userLoginBg')" mode="widthFix" class="w-full" />
    </view>
    <view class="bg-#fff rounded-t-6 mt--6 z-3 relative h-300 py-7.5 px-3">
      <TnForm ref="formRef" :model="formData" :rules="formRules" label-position="top">
        <TnFormItem label="账号" prop="username">
          <TnInput v-model="formData.username" placeholder="请输入账号" />
        </TnFormItem>

        <TnFormItem label="密码" prop="password">
          <TnInput v-model="formData.password" type="password" placeholder="请输入密码" />
        </TnFormItem>
        <TnFormItem label="" prop="agreement">
          <TnCheckbox v-model="formData.agreement" active-color="#49B9AD">
            <text class="text-3 color-#1C2023">同意协议</text>
            <text class="text-3 color-#49B9AD">《用户隐私政策》</text>
          </TnCheckbox>
        </TnFormItem>

        <TnFormItem>
          <!-- <tn-button type="primary" @click="onSubmit">登录</tn-button> -->
          <view
            class="h-11.25 bg-#49B9AD rounded-2.5 flex justify-center items-center color-#fff text-3.75 mt-7"
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
