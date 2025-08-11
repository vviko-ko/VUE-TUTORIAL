<template>
  <canvas ref="canvas"></canvas>
</template>

<script setup>
import { onMounted, ref } from "vue";
import {
  Chart,
  BarController,
  BarElement,
  CategoryScale,
  LinearScale,
  Title,
  Tooltip,
} from "chart.js";

Chart.register(BarController, BarElement, CategoryScale, LinearScale, Title, Tooltip);

const canvas = ref(null);

onMounted(() => {
  new Chart(canvas.value, {
    type: "bar",
    data: {
      labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
      datasets: [
        {
          label: "Users",
          data: [50, 70, 60, 90, 100, 80],
          backgroundColor: "#10b981",
        },
      ],
    },
  });
});
</script>
