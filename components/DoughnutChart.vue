<template>
  <div class="bg-white dark:bg-backgroundDark p-4 rounded-xl shadow-md">
    <Doughnut :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement
} from 'chart.js'
import { Doughnut } from 'vue-chartjs'

// Register Chart.js modules
ChartJS.register(Title, Tooltip, Legend, ArcElement)

const chartData = {
  labels: ['Marketing', 'Development', 'Support'],
  datasets: [
    {
      label: 'Department Budget',
      data: [300, 500, 200],
      backgroundColor: ['#4f46e5', '#06b6d4', '#f59e0b'],
      hoverOffset: 10
    }
  ]
}

const chartOptions = {
  responsive: true,
  plugins: {
    legend: {
      position: 'bottom',
      labels: {
        color: '#666'
      }
    }
  }
}
</script>
