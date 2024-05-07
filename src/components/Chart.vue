<template>
    <div class="container mx-auto relative overflow-x-auto p-10">
      <canvas ref="lineChart" width="900"></canvas>
    </div>
  </template>
  
  <script>
  import Chart from 'chart.js/auto'; // Import Chart.js
  
  export default {
    data() {
      return {
        chart: null,
      };
    },
    props: ['filteredData', 'showDataset'],
    mounted() {
      this.renderChart();
    },
    methods: {
      renderChart() {
        if (this.chart) {
          this.chart.destroy(); // Destroy existing chart if it exists
        }
        
        const labels = this.filteredData.map(entry => this.formatDate(entry.DateTime)); //labels with formated date from the filteredData prop
        const datasets = [
        {
          label: 'Germany',
          data: this.filteredData.map(entry => entry.ENTSOE_DE_DAM_Price), // data from the filteredData prop with the key: ENTSOE_DE_DAM_Price 
          borderColor: '#55cbd3',
          fill: false,
          hidden: !this.showDataset.ENTSOE_DE_DAM_Price // hides/shows dataset based on the showDataset set/ updates when corresponding checkbox is checked/unchecked  
        },
        {
          label: 'Greece',
          data: this.filteredData.map(entry => entry.ENTSOE_GR_DAM_Price),
          borderColor: '#ffb68c',
          fill: false,
          hidden: !this.showDataset.ENTSOE_GR_DAM_Price
        },
        {
          label: 'France',
          data: this.filteredData.map(entry => entry.ENTSOE_FR_DAM_Price),
          borderColor: '#ff6787',
          fill: false,
          hidden: !this.showDataset.ENTSOE_FR_DAM_Price
        }
      ];

        this.chart = new Chart(this.$refs.lineChart, {
          type: 'line',
          data: {
            labels: labels,
            datasets: datasets     
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            interaction: {
              mode: 'index' // show all dataset values when hovering on the line chart
            }
          }
        });
      },
      formatDate(dateTime) { // format iso date to en-US
            return new Date(dateTime).toLocaleString('en-US', { dateStyle: 'medium', timeStyle: 'short' });
        } 
    },
    watch: {
      filteredData: {
        handler() {
          this.renderChart(); // Re-render the chart when timeSeriesData changes
        },
        deep: true
      },
      showDataset: {
        deep: true,
        handler() {
          this.renderChart(); // Re-render the chart when showDataset changes
        }
    }
    },
  };
  </script>