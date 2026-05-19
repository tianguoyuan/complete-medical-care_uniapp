<script lang="ts" setup>
import type { FormItemRule, TnFormInstance } from '@tuniao/tnui-vue3-uniapp'
import type { Arrayable } from '@tuniao/tnui-vue3-uniapp/utils'

import TnButton from '@tuniao/tnui-vue3-uniapp/components/button/src/button.vue'
import TnDateTimePicker from '@tuniao/tnui-vue3-uniapp/components/date-time-picker/src/date-time-picker.vue'
import TnFormItem from '@tuniao/tnui-vue3-uniapp/components/form/src/form-item.vue'
import TnForm from '@tuniao/tnui-vue3-uniapp/components/form/src/form.vue'
import TnInput from '@tuniao/tnui-vue3-uniapp/components/input/src/input.vue'
import TnPicker from '@tuniao/tnui-vue3-uniapp/components/picker/src/picker.vue'
import { computed, ref } from 'vue'

export interface FormConfig {
  config: FormItemConfig[]
  rules?: Partial<Record<string, Arrayable<FormItemRule>>>
}

export interface FormItemConfig {
  label: string
  mode?: 'time' | 'date' | 'datetime' | 'year' | 'yearmonth'
  open?: boolean
  options?: { label: string; value: any }[] // 仅 select 类型使用
  placeholder?: string
  prop: string
  type: 'input' | 'select' | 'date' | 'datetime' | 'phone'
}

const props = withDefaults(
  defineProps<{
    modelValue: Record<string, any>
    config: FormItemConfig[]
    rules?: Partial<Record<string, Arrayable<FormItemRule>>>
  }>(),
  {},
)

const formRef = ref<TnFormInstance | null>(null)
// 暴露验证方法
const validate = () => {}

const resetFields = () => {
  formRef.value?.resetFields()
}

defineExpose({
  resetFields,
  validate,
})
</script>

<template>
  <!-- 
    重要：tn-form 绑定的 :model 必须是响应式的。
    由于我们通过 emit 更新父组件的 modelValue，父组件更新后，新的 modelValue 会传下来。
    这可能导致 tn-form 失去焦点时的实时验证体验稍差，但能消除 mutation 警告。
  -->

  <TnForm
    ref="formRef"
    label-position="left"
    label-width="80px"
    :model="modelValue"
    :rules="props.rules"
    size="sm"
  >
    <TnFormItem
      v-for="(item, index) in props.config"
      :key="index"
      :label="item.label"
      :prop="item.prop"
    >
      <TnInput
        v-if="item.type === 'input'"
        v-model="modelValue[item.prop]"
        :placeholder="item.placeholder"
      />
      <template v-else-if="item.type === 'select'">
        <TnInput
          v-model="modelValue[item.prop]"
          :placeholder="item.placeholder"
          type="select"
          @click="item.open = true"
        />
        <TnPicker
          v-model="modelValue[item.prop]"
          v-model:open="item.open"
          :data="item.options || []"
        />
      </template>
      <template v-else-if="item.type === 'date'">
        <TnInput
          v-model="modelValue[item.prop]"
          :placeholder="item.placeholder"
          type="select"
          @click="item.open = true"
        />
        <TnDateTimePicker
          v-model="modelValue[item.prop]"
          v-model:open="item.open"
          :mode="item.mode || 'date'"
        />
      </template>
    </TnFormItem>
  </TnForm>
</template>

<style lang="scss" scoped>
.w-full {
  width: 100%;
}
</style>
