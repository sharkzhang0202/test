<script setup lang="ts">
import * as echarts from 'echarts'
import type { ECOption } from '~/widgets/guodu-echarts/echarts'

const chartData1 = ref<ECOption>({
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // 坐标轴指示器，坐标轴触发有效
      type: 'shadow', // 默认为直线，可选为：'line' | 'shadow'
    },
    confine: true,
  },
  legend: {
    data: ['销量', '收入'],
  },
  grid: {
    left: 20,
    right: 20,
    bottom: 15,
    top: 40,
    containLabel: true,
  },
  xAxis: {
    type: 'category',
    data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
  },
  yAxis: {
    type: 'value',
  },
  series: [
    {
      name: '销量',
      data: [20, 30, 40, 50, 60, 70, 80],
      type: 'bar',
      showBackground: true,
    },
    {
      name: '收入',
      data: [30, 40, 50, 60, 70, 80, 90],
      type: 'bar',
      showBackground: true,
    },
  ],
})
// setTimeout(() => {
//   // eslint-disable-next-line ts/ban-ts-comment
//   // @ts-expect-error
//   chartData1.value.series[0].data = [51, 130, 50, 40, 60, 80, 55]
// }, 2000)
</script>

<template>
  <view class="bg-[#f5f5f9]">
    <view class="px-30rpx bg-[#00A76E] color-white h-[540rpx] w-[750rpx]">
      <view class="mb-45rpx">
        <GuoduNavBar title="批改详情" :show-back="true">
          <template #icon>
            返回
          </template>
        </GuoduNavBar>
      </view>
      <view class="mb-20rpx flex items-center">
        <view class="mr-20rpx text-32rpx font-bold text-white">
          10/07·初中数学
        </view>
        <view class="b b-1 b-[#fff] rounded-22rpx b-solid text-20rpx font-bold flex-center h-44rpx w-120rpx">
          基础作业
        </view>
      </view>
      <view class="flex justify-between">
        <view class="text-24rpx text-white">
          <view class="my-37rpx">
            班级：五年级一班 数学
          </view>
          <view>
            辅码：一人一码
          </view>
          <view class="my-37rpx">
            时间：10/10 12:00 - 10/20 12:00
          </view>
        </view>
        <view />
      </view>
    </view>
    <view class="transform-translate-y-[-20rpx]">
      <view class="pb-35rpx pt-50rpx mb-25rpx bg-white rounded-30rpx">
        <view class="px-30rpx flex justify-between items-center">
          <view class="text-30rpx font-bold text-[#000333]">
            数据统计
          </view>
          <view class="text-22rpx text-[#8F9AA8]">
            左右滑动可查看更多数据~
          </view>
        </view>
        <view class="h-310rpx w-full">
          <GuoduEcharts
            ref="echarts"
            :options="chartData1" canvas-id="chartData1"
          />
        </view>
      </view>
      <view class="px-30rpx pb-35rpx pt-35rpx mb-25rpx bg-white rounded-30rpx">
        <view class="mb-35rpx flex justify-between items-center">
          <view class="text-30rpx font-bold text-[#000333]">
            最高得分率
          </view>
          <view class="text-38rpx font-bold text-#00A76E relative">
            75%
            <view class="bg-#E7F3EF absolute h-6rpx bottom-4rpx left-0 right-0 z--1" />
          </view>
        </view>
        <view class="grid grid-cols-3 gap-150rpx gap-y-40rpx">
          <view v-for="item in 2" :key="item" class="flex items-center">
            <view class="i-carbon-user-filled text-27rpx text-#A9BCD3" />
            <view class="ml-18rpx text-28rpx text-#465A7B">
              小陈{{ item }}
            </view>
          </view>
        </view>
      </view>
      <view class="px-30rpx pb-35rpx pt-35rpx mb-25rpx bg-white rounded-30rpx">
        <view class="mb-35rpx flex justify-between items-center">
          <view class="text-30rpx font-bold text-[#000333]">
            最低得分率
          </view>
          <view class="text-38rpx font-bold text-#FC5260 relative">
            35%
            <view class="bg-#F6E6E8 absolute h-6rpx bottom-4rpx left-0 right-0 z--1" />
          </view>
        </view>
        <view class="grid grid-cols-3 gap-150rpx gap-y-40rpx">
          <view v-for="item in 3" :key="item" class="flex items-center">
            <view class="i-carbon-user-filled text-27rpx text-#A9BCD3" />
            <view class="ml-18rpx text-28rpx text-#465A7B">
              小陈{{ item }}
            </view>
          </view>
        </view>
      </view>
      <view class="px-30rpx pb-100rpx pt-35rpx bg-white rounded-30rpx rounded-b-none">
        <view class="mb-40rpx flex gap-40rpx items-center">
          <view class="text-28rpx font-bold text-#00A76E">
            有错
            <view class="mx-auto mt-15rpx bg-#00A76E rounded-3rpx h-6rpx w-80%" />
          </view>
          <view class="text-28rpx font-bold text-#000333">
            全对
            <view class="mx-auto mt-15rpx opacity-0 bg-#00A76E rounded-3rpx h-6rpx w-80%" />
          </view>
          <view class="text-28rpx font-bold text-#000333">
            部分批改
            <view class="mx-auto mt-15rpx opacity-0 bg-#00A76E rounded-3rpx h-6rpx w-80%" />
          </view>
          <view class="text-28rpx font-bold text-#000333">
            未批改
            <view class="mx-auto mt-15rpx opacity-0 bg-#00A76E rounded-3rpx h-6rpx w-80%" />
          </view>
        </view>
        <view class="py-22rpx b b-b-#E8EAF1 b-none b-solid b-l-none b-r-none b-t-none text-24rpx text-#8F9AA8 flex justify-between">
          <view class="flex-1">
            学生姓名
          </view>
          <view class="flex-1">
            批改状态
          </view>
          <view class="text-center">
            正确率
          </view>
        </view>
        <view class="py-28rpx b b-b-#E8EAF1 b-none b-solid b-l-none b-r-none b-t-none text-24rpx text-#000333 flex justify-between">
          <view class="flex-1">
            周小虎
          </view>
          <view class="flex-1">
            鲁迅
          </view>
          <view class="text-center">
            10%
          </view>
        </view>
      </view>
    </view>
  </view>
</template>
