<script lang="ts" setup>
import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'
import { ref } from 'vue'

// 引入组件和类型定义
import FormGenerate, { type FormConfig } from '@/components/FormGenerate.vue'
import Navbar from '@/components/Navbar.vue'

// 1. 定义表单数据 (必须使用 ref 或 reactive)
const formData = ref({
  birthday: '', // 对应 date
  gender: '', // 对应 select
  idCard: '',
  name: '',
  phone: '',
  visitTime: '', // 对应 datetime
})

// 2. 定义表单配置
const formConfig = ref<FormConfig>({
  config: [
    {
      label: '姓名',
      placeholder: '请输入姓名',
      prop: 'name',
      type: 'input',
    },
    {
      label: '身份证号',
      placeholder: '请输入身份证号',
      prop: 'idCard',
      type: 'input',
    },
    {
      label: '手机号',
      placeholder: '请输入手机号',
      prop: 'phone',
      type: 'phone', // 专用手机号类型，唤起数字键盘
    },
    {
      label: '性别',
      open: false,
      options: [
        { label: '男', value: 'male' },
        { label: '女', value: 'female' },
      ],
      placeholder: '请选择性别',
      prop: 'gender',
      type: 'select', // 下拉选择
    },
    {
      label: '出生日期',
      open: false,
      placeholder: '请选择出生日期',
      prop: 'birthday',
      type: 'date', // 日期选择器
    },
    {
      label: '就诊时间',
      open: false,
      placeholder: '请选择就诊时间',
      prop: 'visitTime',
      type: 'datetime', // 日期时间选择器
    },
  ],
  rules: {
    name: [
      {
        message: '请输入用户名',
        required: true,
        trigger: 'blur',
      },
      {
        max: 5,
        message: '长度在 3 到 5 个字符',
        min: 3,
        trigger: 'blur',
      },
    ],
  },
})

// 3. 获取组件实例用于验证
const formRef = ref<InstanceType<typeof FormGenerate> | null>(null)

// 4. 提交处理
const handleSubmit = async () => {
  try {
    // 触发表单验证
    await formRef.value?.validate()

    uni.showToast({ icon: 'success', title: '验证通过' })
    console.log('最终提交的数据:', formData.value)

    // TODO: 在这里调用 API 提交 formData.value
  } catch (error) {
    uni.showToast({ icon: 'none', title: '请检查填写内容' })
    console.error('验证失败:', error)
  }
}
</script>

<template>
  <view class="min-h-screen bg-gray-50">
    <Navbar show-back-icon title="新建居民档案" />

    <view class="p-4 bg-white">
      <view class="text-lg font-bold mb-4 text-gray-800">基本信息录入</view>

      <!-- 白色背景卡片包裹表单，更美观 -->
      <view class="rounded-xl shadow-sm">
        <FormGenerate ref="formRef" v-model="formData" v-bind="formConfig" />
      </view>

      <view class="mt-6">
        <tn-button block shape="round" type="primary" @click="handleSubmit">保存提交</tn-button>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
/* 样式可根据需要调整 */
</style>
