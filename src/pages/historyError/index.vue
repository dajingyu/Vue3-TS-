<template>
  <view class="index-page">
    <u-form :model="data.formData" ref="formCheck" :error-type="errorType" label-width="140rpx" :border-bottom=false>
      <view @click="data.formData.show = true">22</view>
      <u-picker
        v-model="data.formData.show"
        mode="time"
        @confirm="confirm"
        :params="params"
      ></u-picker>
      <u-form-item label="时间" prop="time">
        {{ data.formData.time }}
      </u-form-item>
      <u-form-item label="地点" prop="intro" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
      /></u-form-item>

      <u-form-item label="车号" prop="intro2" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
      /></u-form-item>
      <u-form-item label="车序" prop="intro3" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
      /></u-form-item>
      <u-form-item label="异常方位" prop="intro4" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
      /></u-form-item>
      <u-form-item label="异常类型" prop="intro5" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
      /></u-form-item>
      <u-form-item label="备注" prop="intro6" :border-bottom=false
        ><u-input v-model="data.formData.intro" border
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
const confirm = (params) => {
  data.formData.time = `${params.year}-${params.month}-${params.day} ${params.hour}:${params.minute}:${params.second}`
}
let params = {
  year: true,
  month: true,
  day: true,
  hour: true,
  minute: true,
  second: true,
  province: false,
  city: false,
  area: false,
  timestamp: false // 1.3.7版本提供
}
const data = reactive({
  formData: {
    show: false,
    time: '',
    intro: '',
    intro2: '',
    intro3: '',
    intro4: '',
    intro5: '',
    intro6: ''
  },
  rules: {
    name: [
      {
        required: true,
        message: '请输入时间',
        // 可以单个或者同时写两个触发验证方式
        trigger: ['change', 'blur']
      }
    ]
  }
})

onReady(() => {
  formCheck.value.setRules(data.rules)
})

const submit = (e) => {
  formCheck.value.validate((valid) => {
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
