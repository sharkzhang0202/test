<script setup lang="ts">
import { useFetchPage } from '~/composables/useFetchPage'
import { api } from '~/config/api'

// 自定义头部
const tops = ref(0)
const height = ref(0)
onReady(() => {
  uni.getSystemInfo({
    success: (e) => {
      tops.value = e.statusBarHeight || 0
      const custom = uni.getMenuButtonBoundingClientRect()
      height.value = custom.height + (custom.top - (e.statusBarHeight || 0)) * 2
    },
  })
})

// 选择日期代码逻辑
function getDate(type: string) {
  const date = new Date()
  let year = date.getFullYear()
  const month = date.getMonth() + 1
  if (type === 'start')
    year = year - 60
  else if (type === 'end')
    year = year + 2
  return `${year}/${month > 9 ? month : `0${month}`}`
}
const selectDate = ref(getDate(''))
const startDate = computed(() => getDate('start'))
const endDate = computed(() => getDate('end'))
function handleSelectDate(e: { detail: { value: string } }) {
  selectDate.value = e.detail.value.replace('-', '/')
}
interface HomeWorkList {
  day: number
  count: number
}
watch(selectDate, (value: string) => {
  const [year, month] = value.split('/')
  // 请求相关的
})

// 选择班级代码逻辑
const selectClass = ref('全部班级')
const classList = ref<Array<string>>(['全部班级', '一班', '二班'])
function handleSelectClass(e: { detail: { value: number } }) {
  selectClass.value = classList.value[e.detail.value]
}
</script>

<template>
  <view class="page-index top-bg pb-30rpx bg-[#f5f5f9] relative">
    <!-- 顶部日期部分 -->
    <view>
      <!-- 自定义头部导航栏 -->
      <view class="px-[30rpx] mb-[25rpx]">
        <view :style="[tops ? `height:${tops}px` : `height: 1.2rem`]" />
        <view class="text-40 font-bold h-38" :style="[height ? `height:${height}px; line-height: ${height}px` : `height: auto; line-height: normal`]">
          智慧作业教师端
        </view>
      </view>
      <!-- 选择年月 -->
      <view class="px-[30rpx] mb-[30rpx] flex justify-between items-center">
        <view class="flex items-center">
          <text class="text-38 font-bold color-[#000333]">
            <picker mode="date" :value="selectDate" :start="startDate" :end="endDate" fields="month" @change="handleSelectDate">
              <view class="uni-input">
                {{ selectDate }}
              </view>
            </picker>
          </text>
          <view class="i-carbon-chevron-down ml-[17rpx] text-28 text-[#778496]" />
        </view>
        <view class="p-x-[23rpx] bg-[#ffffff66] b b-[2px] border-[#fff] rounded-[18rpx] border-solid h-70 w-250 box-border">
          <picker mode="selector" :value="selectClass" :range="classList" @change="handleSelectClass">
            <view class="flex h-66 justify-between items-center">
              <text class="text-26">
                {{ selectClass }}
              </text>
              <view class="i-carbon-chevron-down text-20 text-[#778496]" />
            </view>
          </picker>
        </view>
      </view>
      <!-- 选择天 -->
      <view class="mb-[30rpx]">
        <scroll-view class="whitespace-nowrap" scroll-x :show-scrollbar="false">
          <view v-for="item in 29" :key="item" class="day-item mx-[10rpx] inline-block">
            <view class="mx-auto bg-[#00A76E] rounded-[20rpx] text-[36rpx] font-bold line-height-[66rpx] text-center text-white h-[66rpx] w-[66rpx]">
              {{ item }}
            </view>
            <view class="mx-auto mb-[5rpx] mt-[10rpx] bg-[#00A76E] rounded-1/2 h-[12rpx] w-[12rpx]" />
            <view class="text-[22rpx] line-height-[34rpx] text-center text-[#000333]">
              5份作业
            </view>
          </view>
        </scroll-view>
      </view>
      <view />
    </view>
    <!-- 中间功能模块 -->
    <view class="px-[30rpx] mb-[30rpx] grid grid-cols-4 gap-y-[30rpx]">
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section1.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          发布作业
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section2.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          批改作业
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section3.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          发布学习计划
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section4.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          共性错题分析
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section5.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          离线批改
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section6.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          学情分析
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section7.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          挑题组卷
        </view>
      </view>
      <view>
        <view class="mx-auto h-100 w-120">
          <image class="h-full w-full" src="..\..\static\icon\index-setion\section8.png" mode="aspectFill" />
        </view>
        <view class="mt-[17rpx] text-[22rpx] text-center text-[#000333]">
          我的积分
        </view>
      </view>
    </view>
    <!-- 底部作业列表模块 -->
    <view class="px-[30rpx]">
      <view v-for="item in 4" :key="item" class="mb-[30rpx]">
        <card-homework />
      </view>
      <GuoduEmpty message="今天没有布置作业" />
    </view>
  </view>
</template>

<style lang="scss">
.page-index {
  .day-item {
    &:first-child {
      margin-left: 30rpx;
    }
    &:last-child {
      margin-right: 30rpx;
    }
  }
}
</style>
