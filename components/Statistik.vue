<template>
  <div>
    <canvas id="statistik"></canvas>
  </div>
</template>

<script setup>
import Chart from 'chart.js/auto'

const labels = [
  'January',
  'February',
  'March',
  'April',
  'May',
  'June',
];

const data = {
  labels: labels,
  datasets: [{
    label: 'Pengunjung',
    backgroundColor:  'rgba(255, 100, 20, 0.2)',
    borderColor: 'rgb(0,0,0)',
    borderWidth: 1,
    data: [30, 40, 50, 40, 20, 50],
  }]
};

const config = {
  type: 'bar',
  data: data,
  options: {}
};

onMounted(() => {
  const myChart = new Chart(
    document.getElementById('statistik'),
    config
  );
})
</script>
