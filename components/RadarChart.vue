<template>
  <div class="bg-white dark:bg-backgroundDark p-4 rounded-xl shadow-md">
    <Radar :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  RadialLinearScale,
  PointElement,
  LineElement,
  Filler
} from 'chart.js'
import { Radar } from 'vue-chartjs'

// Register Chart.js modules
ChartJS.register(
  Title, Tooltip, Legend,
  RadialLinearScale, PointElement, LineElement, Filler
)

const chartData = {
  labels: ['Speed', 'Reliability', 'Comfort', 'Safety', 'Efficiency', 'Style'],
  datasets: [
    {
      label: 'Car A',
      data: [65, 59, 90, 81, 56, 55],
      fill: true,
      backgroundColor: 'rgba(79,70,229,0.2)',
      borderColor: '#4f46e5',
      pointBackgroundColor: '#4f46e5'
    },
    {
      label: 'Car B',
      data: [28, 48, 40, 19, 96, 27],
      fill: true,
      backgroundColor: 'rgba(6,182,212,0.2)',
      borderColor: '#06b6d4',
      pointBackgroundColor: '#06b6d4'
    }
  ]
}

const chartOptions = {
  responsive: true,
  plugins: {
    legend: {
      position: 'top',
      labels: {
        color: '#666'
      }
    }
  },
  scales: {
    r: {
      angleLines: { color: '#ccc' },
      grid: { color: '#eee' },
      pointLabels: { color: '#666' }
    }
  }
}
</script>
