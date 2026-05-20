<script lang="ts" setup>
import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'
import { ref } from 'vue'

// 引入组件和类型定义
import FormGenerate, { type FormConfig } from '@/components/FormGenerate.vue'
import Navbar from '@/components/Navbar.vue'

// 1. 定义表单数据 (必须使用 ref 或 reactive)
const formData = ref({
  birthday: '',
  customTag: [],
  familyMember: [],
  gender: '',
  idCard: '',
  name: '',
  phone: '',
  province: ['11', '1101', '110109'], // 对应 datetime
  sign: true,
  tag: '',
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
      label: '日期',
      open: false,
      placeholder: '请选择出生日期',
      prop: 'birthday',
      type: 'date', // 日期选择器
    },
    {
      inputType: 'number',
      label: '联系电话',
      placeholder: '请输入联系电话',
      prop: 'phone',
      type: 'input',
    },
    {
      label: '现居地',
      placeholder: '请选择现居地',
      prop: 'province',
      type: 'regionPicker',
    },
    {
      label: '居民标签',
      placeholder: '请输入居民标签',
      prop: 'tag',
      type: 'input',
    },
    {
      border: true,
      label: '自定义标签',
      options: [
        {
          label: '高血压',
          value: '1',
        },
        {
          label: '冠心病',
          value: '2',
        },
        {
          label: '高血脂',
          value: '3',
        },
        {
          label: '糖尿病',
          value: '4',
        },
        {
          label: '高血糖',
          value: '5',
        },
        {
          label: '低血糖',
          value: '6',
        },
      ],
      placeholder: '请选择居民标签',
      prop: 'customTag',
      type: 'checkbox',
    },
    {
      label: '关联家人',
      options: [
        {
          label: '张三',
          value: '张三',
        },
        {
          label: '李四',
          value: '李四',
        },
      ],
      placeholder: '请选择关联家人',
      prop: 'familyMember',
      type: 'select',
    },
    {
      label: '立即签约',
      prop: 'sign',
      type: 'switch',
    },
  ],
  rules: {
    birthday: [
      {
        message: '请输入性别',
        required: true,
        trigger: 'blur',
      },
    ],
    familyMember: [
      {
        message: '请输入关系',
        required: true,
        trigger: 'change',
      },
    ],
    gender: [
      {
        message: '请输入性别',
        required: true,
        trigger: 'change',
      },
    ],

    idCard: [
      {
        message: '请输入身份证号',
        required: true,
        trigger: 'blur',
      },
      {
        message: '请输入有效的身份证号',
        pattern: /(^\d{15}$)|(^\d{17}([0-9]|X|x)$)/,
        trigger: 'blur',
      },
    ],
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
    phone: [
      {
        message: '请输入有效的联系电话',
        pattern: /^1[3-9]\d{9}$/,
        required: true,
        trigger: 'blur',
      },
    ],
    province: [
      {
        message: '请选择现居地',
        required: true,
        trigger: 'change',
      },
    ],
    sign: [
      {
        message: '请确认是否签约',
        required: false,
        trigger: 'change',
      },
    ],
    tag: [
      {
        message: '请输入标签',
        required: true,
        trigger: 'change',
      },
    ],
  },
})

// 3. 获取组件实例用于验证
const formGenerateRef = ref<InstanceType<typeof FormGenerate> | null>(null)

// 4. 提交处理
async function handleSubmit() {
  // 触发表单验证
  await formGenerateRef.value?.validate()

  console.log('formData', formData.value)

  uni.navigateTo({
    url: '/pages/home/editSignInfo',
  })
}
</script>

<template>
  <view class="min-h-screen">
    <Navbar fixed show-back-icon show-home-icon title="新建居民档案" />
    <view class="bg-white p-4 pb-10">
      <view class="mb-4 text-lg text-gray-800 font-bold">基本信息录入</view>

      <!-- 白色背景卡片包裹表单，更美观 -->
      <view class="rounded-xl">
        <FormGenerate ref="formGenerateRef" v-model="formData" v-bind="formConfig" />
      </view>

      <view class="mt-10">
        <view
          class="h-10 w-full flex items-center justify-center rounded-2.5 bg-#49B9AD color-#fff"
          @click="handleSubmit"
        >
          下一步
        </view>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
/* 样式可根据需要调整 */
</style>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: '新建居民档案',
  },
  needLogin: false,
}
</route>
