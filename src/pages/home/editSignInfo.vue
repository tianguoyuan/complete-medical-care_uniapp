<script lang="ts" setup>
import FormGenerate from '@/components/FormGenerate.vue'
import { type FormConfig } from '@/components/FormGenerate.vue'
import Navbar from '@/components/Navbar.vue'

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
      label: '签约机构',
      placeholder: '请输入签约机构',
      prop: 'field1',
      type: 'input',
    },
    {
      label: '签约团队',
      placeholder: '请输入签约团队',
      prop: 'field2',
      type: 'input',
    },
    {
      label: '签约医生',
      placeholder: '请输入签约医生',
      prop: 'idCard',
      type: 'input',
    },
    {
      label: '服务包',
      placeholder: '请输入服务包',
      prop: 'field3',
      type: 'input',
    },
    {
      label: '签约周期',
      placeholder: '请输入签约周期',
      prop: 'field4',
      type: 'input',
    },
    {
      label: '费用',
      placeholder: '请输入费用',
      prop: 'field5',
      type: 'input',
    },
    {
      inputType: 'textarea',
      label: '备注',
      placeholder: '请输入备注',
      prop: 'field6',
      type: 'input',
    },
  ],
})

// 3. 获取组件实例用于验证
const formGenerateRef = ref<InstanceType<typeof FormGenerate> | null>(null)

// 4. 提交处理
async function handleSubmit() {
  // 触发表单验证
  await formGenerateRef.value?.validate()

  console.log('formData', formData.value)

  uni.navigateTo({
    url: '/pages/home/submitSignInfo',
  })
}
</script>

<template>
  <view class="">
    <Navbar fixed show-back-icon show-home-icon title="新建居民档案" />
    <view class="bg-white p-4 pb-10">
      <view class="mb-4 text-lg text-gray-800 font-bold">签约信息</view>
      <view class="rounded-xl">
        <FormGenerate ref="formGenerateRef" v-model="formData" v-bind="formConfig" />
      </view>

      <view class="mt-10">
        <view
          class="h-10 w-full flex items-center justify-center rounded-2.5 bg-#49B9AD color-#fff"
          @click="handleSubmit"
        >
          确定
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
    navigationBarTitleText: '填写签约信息',
  },
}
</route>
