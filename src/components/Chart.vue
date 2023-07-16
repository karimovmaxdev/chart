<script setup lang="ts">
import Chart from 'chart.js/auto';
import { ref, watch, computed } from 'vue';
import {ChartDatasetCustomTypesPerDataset} from 'chart.js'

const props = defineProps<{ data: any }>();
const data = computed(() => props.data);
const chart:any = ref(false)

watch(data, () => {
  if(chart.value) {
    chart.value.destroy()
  }
  if(!data.value.length) return;

  const ctx = document.getElementById('myChart') as HTMLCanvasElement;
  const object: any = {};

  const keys = Object.keys(data.value[0]);
  keys.forEach((it: string) => {
    object[it] = {
      label: it,
      data: [],
      borderWidth: 1,
      borderColor: '#'+(Math.random() * 0xFFFFFF << 0).toString(16).padStart(6, '0')
    }
  })

  
  data.value.forEach((item: Object, index: number) => {
    if(index === 0) return;
    const entries = Object.entries(item);
    entries.forEach(it => {
      object[it[0]].data.push(isNaN(it[1]) ? 0 : Number(it[1].slice(0,2)))
    })
  })
  
  const datasets: ChartDatasetCustomTypesPerDataset[] = Object.values(object)
  
  chart.value = new Chart(ctx, {
    type: 'line',
    data: {
      labels: ['2010', '2012', '2014', '2016', '2018', '2020', '2022'],
      datasets: [
        ...datasets
      ]
    },
    options: {
      scales: {
        y: {
          beginAtZero: true
        },
      }
    }
  });
})



  

</script>

<template>
  <div>
    <canvas id="myChart"></canvas>
  </div>

</template>

<style scoped>
</style>
