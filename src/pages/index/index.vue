<script setup lang="ts">
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

function getDate(type: string) {
  const date = new Date()
  let year = date.getFullYear()
  let month = date.getMonth() + 1

  if (type === 'start')
    year = year - 60
  else if (type === 'end')
    year = year + 2

  month = Number(month > 9 ? month : `0${month}`)
  return `${year}-${month}`
}
const selectTime = ref(getDate(''))
const startDate = computed(() => {
  return getDate('start')
})
const endDate = computed(() => {
  return getDate('end')
})

function handleSelectTime(e: { detail: { value: string } }) {
  selectTime.value = e.detail.value
}
</script>

<template>
  <view class="index-bg px-[30rpx] pb-30rpx bg-[#f5f5f9] relative">
    <!-- 顶部日期部分 -->
    <view>
      <!-- 自定义头部导航栏 -->
      <view class="mb-[25rpx]">
        <view :style="[tops ? `height:${tops}px` : `height: 1.5rem`]" />
        <view class="text-size-40 font-bold h-38" :style="[height ? `height:${height}px; line-height: ${height}px` : `height: auto; line-height: normal`]">
          智慧作业教师端
        </view>
      </view>
      <!-- 选择年月 -->
      <view class="mb-[30rpx] flex justify-between items-center">
        <view class="flex items-center">
          <text class="text-38 font-bold color-[#000333]">
            <picker mode="date" :value="selectTime" :start="startDate" :end="endDate" fields="month" @change="handleSelectTime">
              <view class="uni-input">
                {{ selectTime }}
              </view>
            </picker>
          </text>
          <view class="i-carbon-chevron-down ml-[17rpx] text-28 text-[#778496]" />
        </view>
        <view class="p-x-[23rpx] bg-[#ffffff66] b b-[2px] border-[#fff] rounded-[18rpx] border-solid h-70 w-250 box-border">
          <picker mode="selector">
            <view class="flex h-66 justify-between items-center">
              <text class="text-26">
                全部班级
              </text>
              <view class="i-carbon-chevron-down text-20 text-[#778496]" />
            </view>
          </picker>
        </view>
      </view>
      <!-- 选择天 -->
      <view class="mb-[30rpx]">
        <scroll-view class="whitespace-nowrap" scroll-x :show-scrollbar="false">
          <view v-for="item in 29" :key="item" class="mx-[10rpx] inline-block">
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
    <view class="mb-[30rpx] grid grid-cols-4 gap-y-[30rpx]">
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
    <view>
      <view v-for="item in 4" :key="item" class="mb-[30rpx]">
        <card-homework />
      </view>
    </view>
  </view>
</template>

<style lang="scss">
</style>
