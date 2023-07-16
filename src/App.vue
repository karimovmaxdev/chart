<script setup lang="ts">
import { ref, computed } from 'vue';
import InputForChart from './components/InputForChart.vue';
import Chart from './components/Chart.vue'

const data = ref([]);
const array = computed(() => data.value)

function dataSubmit(value: []) {
  data.value = value
}
</script>

<template>
  <Chart :data="array"/>
  <InputForChart @data-submit="dataSubmit"/>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
