<template>
  <div>
    <Navbar />
 

    <!-- Year and Month Filter Section -->
    <div class="filter-container">
      <!-- <label for="yearSelect">Select Year:</label> -->
      <select v-model="selectedYear" id="yearSelect" @change="drawCharts">
        <option value="" disabled>Select a Year</option>
        <option v-for="year in availableYears" :key="year" :value="year">{{ year }}</option>
      </select>

      <!-- <label for="monthSelect">Select Month:</label> -->
      <select v-model="selectedMonth" id="monthSelect" @change="drawCharts">
        <option value="" disabled>Select a Month</option>
        <option v-for="month in availableMonths" :key="month" :value="month">{{ month }}</option>
      </select>
    </div>

    <!-- Grid Container for Charts -->
    <div class="grid-container">
      <div class="chart-section large-chart" ref="chart1"></div> <!-- First chart section -->
      <div class="chart-section large-chart" ref="chart2"></div> <!-- Second chart section -->
      <div class="chart-section small-chart" ref="chart3"></div> <!-- Third chart section (Pie Chart) -->
      <div class="chart-section small-chart" ref="chart4"></div> <!-- Fourth chart section (Pie Chart) -->
    </div>
  </div>
</template>

<script>
import Navbar from '../components/Navbar.vue';

export default {
  name: 'StatsPage',
  components: {
    Navbar,
  },
  data() {
    return {
      selectedYear: '', // For storing the selected year
      selectedMonth: '', // For storing the selected month
      availableYears: ['2019', '2020', '2021', '2022', '2023'], // Available years for the dropdown
      availableMonths: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'], // Available months for the dropdown
    };
  },
  mounted() {
    // Load the Google Charts library
    this.loadGoogleCharts();
  },
  methods: {
    loadGoogleCharts() {
      if (typeof window.google === 'undefined') {
        const script = document.createElement('script');
        script.src = 'https://www.gstatic.com/charts/loader.js';
        script.onload = () => {
          window.google.charts.load('current', {
            packages: ['corechart', 'bar'],
          });
          window.google.charts.setOnLoadCallback(this.drawCharts);
        };
        document.head.appendChild(script);
      } else {
        window.google.charts.load('current', {
          packages: ['corechart', 'bar'],
        });
        window.google.charts.setOnLoadCallback(this.drawCharts);
      }
    },
    drawCharts() {
      // Prepare data for the first chart
      const data1 = window.google.visualization.arrayToDataTable([
        ['Year', 'Accepted', 'Rejected'],
        ['2019', 300, 50],
        ['2020', 400, 75],
        ['2021', 350, 90],
        ['2022', 500, 60],
        ['2023', 450, 80],
      ]);

      const options1 = {
        title: 'Loan Applications: Accepted vs Rejected (Count)',
        chartArea: { width: '50%' },
        hAxis: {
          title: 'Years',
          minValue: 0,
        },
        vAxis: {
          title: 'Count',
        },
        colors: ['#4caf50', '#f44336'],
      };

      const chart1 = new window.google.visualization.ColumnChart(this.$refs.chart1);
      chart1.draw(data1, options1);

      // Prepare data for the second chart
      const data2 = window.google.visualization.arrayToDataTable([
        ['Year', 'Accepted', 'Rejected'],
        ['2019', 28000000, 4000000],
        ['2020', 35000000, 7000000],
        ['2021', 30000000, 6000000],
        ['2022', 45000000, 5500000],
        ['2023', 40000000, 7000000],
      ]);

      const options2 = {
        title: 'Loan Applications: Accepted vs Rejected (Price)',
        chartArea: { width: '50%' },
        hAxis: {
          title: 'Years',
          minValue: 0,
        },
        vAxis: {
          title: 'Price',
        },
        colors: ['#4caf50', '#f44336'],
      };

      const chart2 = new window.google.visualization.ColumnChart(this.$refs.chart2);
      chart2.draw(data2, options2);

      // Prepare data for the third chart (Pie Chart)
      const data3 = window.google.visualization.arrayToDataTable([
        ['Status', 'Count'],
        ['Approved', 320],
        ['Declined', 60],
      ]);

      const options3 = {
        title: 'Loan Applications: Approved vs Declined (According to the age)',
        pieHole: 0.4, // Creates a donut chart
        colors: ['#2196f3', '#ff9800'],
      };

      const chart3 = new window.google.visualization.PieChart(this.$refs.chart3);
      chart3.draw(data3, options3);

      // Prepare data for the fourth chart (Pie Chart)
      const data4 = window.google.visualization.arrayToDataTable([
        ['Status', 'Count'],
        ['Approved', 290],
        ['Declined', 45],
      ]);

      const options4 = {
        title: 'Loan Applications: Approved vs Declined (According to education level)',
        pieHole: 0.4, // Creates a donut chart
        colors: ['#2196f3', '#ff9800'],
      };

      const chart4 = new window.google.visualization.PieChart(this.$refs.chart4);
      chart4.draw(data4, options4);
    },
  },
};
</script>

<style scoped>
/* Adjust grid layout and chart sizes */
.grid-container {
  display: grid;
  grid-template-columns: 1fr 1fr; /* Two equal columns */
  grid-template-rows: auto auto; /* Two rows */
  gap: 20px; /* Space between the sections */
  padding: 20px; /* Padding around the container */
}

.large-chart {
  height: 400px; /* Larger height for the column charts */
  width: 100%; /* Full width */
  background-color: #ffffff; /* Set background color */
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.small-chart {
  height: 400px; /* Smaller height for the pie charts */
  width: 100%; /* Full width */
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.filter-container {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-bottom: 20px;
  margin-top: 20px;
}

select {
  padding: 8px;
  border-radius: 4px;
  font-size: 16px;
}
</style>
