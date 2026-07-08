<script lang="ts" setup>
import { useI18n } from 'vue-i18n'

import Navbar from '@/components/Navbar.vue'
import { useAppStore } from '@/store/app'

const appStore = useAppStore()
const { locale, t } = useI18n()

function switchLang() {
  locale.value = locale.value === 'zh-Hans' ? 'en' : 'zh-Hans'
}
</script>

<template>
  <view
    class="bg-#fcfcfc"
    :style="{
      'min-height': `${appStore.systemScreenHeight}px`,
    }"
  >
    <Navbar showBackIcon showHomeIcon title="Demo" />
    <view>demo - page</view>
    <view class="p-4">
      <view class="mb-4 text-lg font-bold">i18n 示例</view>
      <view class="mb-2">t 用法: {{ t('app.name') }}</view>
      <view class="mb-2">t 用法: {{ t('home.welcome') }}</view>
      <view class="mb-2">登录页: {{ t('login.title') }}</view>
      <view class="mb-4">当前语言: {{ locale }}</view>
      <button class="rounded text-white bg-main" @tap="switchLang">切换语言 / Switch Lang</button>
    </view>
  </view>
</template>

<route lang="json5" type="page">
{
  layout: 'default',
  style: {
    navigationStyle: 'custom',
    navigationBarTitleText: 'demo',
  },
}
</route>
