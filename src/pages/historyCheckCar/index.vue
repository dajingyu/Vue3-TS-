<template>
  <view class="index-page">
    <u-form
      :model="data.formData"
      ref="formCheck"
      :error-type="errorType"
      label-width="140rpx"
      :border-bottom="false"
    >
      <u-picker
        v-model="data.formData.show"
        mode="time"
        @confirm="confirm"
        :params="params"
      ></u-picker>

      <u-picker
        v-model="data.formData.showEndTime"
        mode="time"
        @confirm="endConfirm"
        :params="params"
      ></u-picker>
      <u-form-item label="开始时间" prop="beginTime">
        <view @click="data.formData.show = true">
          {{ data.formData.beginTime }}
        </view>
      </u-form-item>
      <u-form-item label="结束时间" prop="endTime" :border-bottom="false">
        <view @click="data.formData.showEndTime = true">
          {{ data.formData.endTime }}
        </view></u-form-item
      >
    </u-form>

    <u-button @click="submit">检索</u-button>

    <u-table>
      <u-tr>
        <u-th>学校1</u-th>
        <u-th>班级2</u-th>
        <u-th>年龄4</u-th>
        <u-th>年龄3</u-th>
      </u-tr>
      <u-tr v-for="item in list">
        <u-td>{{ item.name }}</u-td>
        <u-td>{{ item.name2 }}</u-td>
        <u-td>{{ item.ame4 }}</u-td>
        <u-td>{{ item.name3 }}</u-td>
      </u-tr>
    </u-table>
  </view>
</template>

<script setup lang="ts">
import { ref, reactive, onMounted, unref, computed, watch } from 'vue'
import { onLoad, onReady } from '@dcloudio/uni-app'
const formCheck = ref()
const errorType = ['toast']

const list = reactive([
  { name: '1', name2: '2', name3: '3', ame4: '4' },
  { name: '1', name2: '2', name3: '3', ame4: '4' },
  { name: '1', name2: '2', name3: '3', ame4: '4' }
])
const data = reactive({
  formData: {
    beginTime: '请选择开始时间',
    endTime: '请选择结束时间',
    show: false,
    showEndTime: false
  },
  rules: {
    name: [
      {
        required: true,
        message: '请输入用户名',
        // 可以单个或者同时写两个触发验证方式
        trigger: ['change', 'blur']
      }
    ]
  }
})

const confirm = (params) => {
  data.formData.beginTime = `${params.year}-${params.month}-${params.day} ${params.hour}:${params.minute}:${params.second}`
}
const endConfirm = (params) => {
  data.formData.endTime = `${params.year}-${params.month}-${params.day} ${params.hour}:${params.minute}:${params.second}`
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
