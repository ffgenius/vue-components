<script setup lang="ts">
import { ref } from 'vue'
import Slider from '../src'

const style = {
  width: '400px',
  margin: '50px',
}

const decimal = ref([0.5, 0.6, 0.7])
const trackClick = ref([20, 40])
const insertHandle = ref([20, 40])
</script>

<template>
  <div :style="style">
    <p>
      小数步长 + pushable：`min=0 max=1 step=0.1 pushable=0.1`。
      拖动任意 handle，相邻间隙应稳定停在 0.1，不会一次跳两格。
    </p>
    <Slider v-model:value="decimal" range :min="0" :max="1" :step="0.1" :pushable="0.1" />
    <div :style="{ fontSize: '12px', color: '#999' }">
      value: {{ decimal }}
    </div>
  </div>

  <div :style="style">
    <p>
      点击轨道 + pushable：点击后所有 handle 的间隔必须 ≥ 20。
      点击轨道中段，结果应是 `[10, 30]` 这类保持间隙的分布。
    </p>
    <Slider v-model:value="trackClick" range :pushable="20" />
    <div :style="{ fontSize: '12px', color: '#999' }">
      value: {{ trackClick }}
    </div>
  </div>

  <div :style="style">
    <p>
      editable + pushable：点击轨道插入新 handle 时同样保持间隙。
      在 `[20, 40]` 上点击中段，应得到 `[10, 30, 50]` 而不是把间隙压到 10。
    </p>
    <Slider v-model:value="insertHandle" :range="{ editable: true }" :pushable="20" />
    <div :style="{ fontSize: '12px', color: '#999' }">
      value: {{ insertHandle }}
    </div>
  </div>
</template>
