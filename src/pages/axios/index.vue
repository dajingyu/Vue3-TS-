<!-- <template>
  <view class="axios-demo">
    <view class="title-h1">Axios Page</view>
    <input type="number" v-model="phone" />
    <button @click="getCode">获取验证码(GET)</button>
  </view>
</template>
<script lang="ts" setup>
import { ref } from 'vue'
import { userApi } from '@/api'

const phone = ref('12345678901')

const getCode = () => {
  userApi
    .getCode(phone.value)
    .then((v) => {
      uni.showToast({
        title: `${v.num}`,
        icon: 'success'
      })
    })
    .catch((err) => {
      console.log(err)
      uni.showToast({
        title: '获取验证码失败',
        icon: 'error'
      })
    })
}
</script>

<style lang="less" scoped>
.axios-demo {
  text-align: center;
}
.title-h1 {
  font-size: 50rpx;
}
</style> -->

<template>
  <view class="index-page">
    <u-form :model="data.formData" ref="formCheck" :error-type="errorType">
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
      <u-form-item label="地点" prop="intro"
        ><u-input v-model="data.formData.intro"
      /></u-form-item>

      <u-form-item label="地点2" prop="intro2"
        ><u-input v-model="data.formData.intro"
      /></u-form-item>
      <u-form-item label="地点3" prop="intro3"
        ><u-input v-model="data.formData.intro"
      /></u-form-item>
      <u-form-item label="照片1" prop="photo"
        ><u-upload
          :action="action"
          :max-size="5 * 1024 * 1024"
          max-count="1"
        ></u-upload
      ></u-form-item>
      <u-form-item label="照片2" prop="photo2"
        ><u-upload
          :action="action"
          :max-size="5 * 1024 * 1024"
          max-count="1"
        ></u-upload
      ></u-form-item>
      <u-form-item label="照片3" prop="photo3"
        ><u-upload
          :action="action"
          :max-size="5 * 1024 * 1024"
          max-count="1"
        ></u-upload
      ></u-form-item>
    </u-form>

    <u-button @click="submit">异常排除</u-button>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, unref, computed, watch } from 'vue'
import { onLoad, onReady } from '@dcloudio/uni-app'
const formCheck = ref()
const errorType = ['toast']
const action = ref('')
const fileList = ref([])

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
    photo: '',
    photo2: '',
    photo3: ''
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
