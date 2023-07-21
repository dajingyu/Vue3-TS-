<template>
  <view class="index-page">
    <u-form :model="data.formData" ref="formCheck" :error-type="errorType">
      <u-form-item label="时间" prop="name"
        ><u-input v-model="data.formData.name"
      /></u-form-item>
      <u-form-item label="地点" prop="intro"
        ><u-input v-model="data.formData.intro"
      /></u-form-item>
    </u-form>

    <u-button @click="submit">异常排除</u-button>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, unref, computed, watch } from 'vue'
import { onLoad, onReady } from '@dcloudio/uni-app'
const formCheck = ref()
const errorType = ['toast']
const data = reactive({
  formData: {
    name: '',
    intro: ''
  },
  rules: {
    name: [
      {
        required: true,
        message: '请输入用户名',
        // 可以单个或者同时写两个触发验证方式
        trigger: ['change', 'blur']
      }
    ],
    intro: [
      {
        required: true,
        min: 5,
        message: '简介不能少于5个字',
        trigger: 'change'
      }
    ]
  }
})

onReady(() => {
  formCheck.value.setRules(data.rules)
})

const submit = (e) => {
  form1.value.validate((valid) => {
    if (valid) {
      uni.showToast({
        title: '请求成功',
        icon: 'none'
      })

      console.log('验证通过')
    } else {
      console.log('验证失败')
    }
  })
}
</script>

<style scoped></style>
