<template>
  <view class="page">
    <view class="header">
      <text class="title">电池包状态</text>
      <button class="refresh" @click="refresh">刷新示例数据</button>
    </view>
    <view class="canvas-wrap">
      <canvas
        id="batteryCanvas"
        canvas-id="batteryCanvas"
        class="battery-canvas"
        @touchstart="onTouchStart"
        @touchmove="onTouchMove"
        @touchend="onTouchEnd"
      />
    </view>
  </view>
</template>

<script>
import { UniBatteryPackRefactored } from 'antbms-battery-pack'

export default {
  data() {
    return {
      pack: null
    }
  },
  onReady() {
    this.pack = new UniBatteryPackRefactored('batteryCanvas', {
      padding: 20,
      batteryWidth: 48,
      batteryHeight: 90,
      batteryGap: 14,
      colors: {
        normal: '#5C8AF0',
        warning: '#f5a742',
        danger: '#f54242',
        passive_balancing: '#ABF04B',
        active_balance_line: '#5C8AF0'
      }
    })
    this.refresh()
  },
  onUnload() {
    if (this.pack) {
      this.pack.destroy()
      this.pack = null
    }
  },
  methods: {
    refresh() {
      const data = []
      for (let i = 1; i <= 12; i++) {
        const voltage = 3.0 + Math.random() * 1.2
        const temperature = 20 + Math.random() * 20
        data.push({
          id: i,
          voltage: voltage.toFixed(3) + 'V',
          temperature: temperature.toFixed(1) + '°C',
          status: voltage < 3.2 ? 'danger' : voltage < 3.5 ? 'warning' : 'normal',
          passiveBalance: i % 4 === 0
        })
      }
      this.pack && this.pack.updateData(data)
    },
    onTouchStart(e) {
      this.pack && this.pack.handleTouchStart(e)
    },
    onTouchMove(e) {
      this.pack && this.pack.handleTouchMove(e)
    },
    onTouchEnd(e) {
      this.pack && this.pack.handleTouchEnd(e)
    }
  }
}
</script>

<style>
.page {
  min-height: 100vh;
  padding: 24rpx;
  box-sizing: border-box;
}
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 24rpx;
}
.title {
  font-size: 36rpx;
  font-weight: 600;
  color: #1f2937;
}
.refresh {
  font-size: 26rpx;
  line-height: 2;
  margin: 0;
}
.canvas-wrap {
  background: #ffffff;
  border-radius: 16rpx;
  padding: 16rpx;
}
.battery-canvas {
  width: 100%;
  height: 600rpx;
}
</style>
