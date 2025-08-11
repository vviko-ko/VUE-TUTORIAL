<template>
  <canvas ref="canvas"></canvas>
</template>

<script setup>
import { onMounted, ref } from "vue";
import {
  Chart,
  LineController,
  LineElement,
  PointElement,
  CategoryScale,
  LinearScale,
  Title,
  Tooltip,
} from "chart.js";

Chart.register(LineController, LineElement, PointElement, CategoryScale, LinearScale, Title, Tooltip);

const canvas = ref(null);

onMounted(() => {
  new Chart(canvas.value, {
    type: "line",
    data: {
      labels: ["Jan", "Feb", "Mar", "Apr", "May", "Jun"],
      datasets: [
        {
          label: "Sales",
          data: [150, 200, 180, 220, 300, 250],
          borderColor: "#3b82f6",
          backgroundColor: "rgba(59,130,246,0.2)",
        },
      ],
    },
  });
});
</script>
