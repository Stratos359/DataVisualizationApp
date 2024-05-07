<template>
  <div class="py-10 bg-sky-50 lg:grid lg:grid-cols-2">
    <div class="mx-10 mb-10 p-5 bg-white border border-gray-20 rounded-lg shadow-2xl">
      <div class="container px-3">
        <div class="flex">
          <div class="pr-2">
            <VueDatePicker v-model="date" placeholder="Select Dates" :enable-time-picker="false" :start-date="new Date(2024,1,1)" :max-date="new Date(2024,1,12)" range auto-apply></VueDatePicker> <!-- Create Date Picker-->
          </div>
          <div v-for="(dataset, key) in datasets" :key="key" class="flex items-center mb-4 pr-2 pt-2"> <!-- Create Checkboxes based on how many elements are on the datasets set-->
            <input type="checkbox" :id="dataset.key" v-model="showDataset[dataset.key]" class="w-4 h-4 text-blue-600 bg-gray-100 border-gray-300 rounded focus:ring-blue-500 focus:ring-2"> <!--Checkboxes change the state of each showDataset set to be passed to the Table and Chart Component-->
            <label class="ms-2 text-sm font-medium text-gray-900 dark:text-gray-300">{{ dataset.label }}</label> <!-- Create dynamic label from the datasets set-->
          </div>
        </div>
          <Table :filteredData="filteredData" :showDataset="showDataset" :datasets="datasets" /> <!-- Create Table with passed props to filter table-->
      </div>
    </div>
    <div class="mx-10 mt-10 bg-white border border-gray-20 rounded-lg shadow-2xl">
      <Chart :filteredData="filteredData" :showDataset="showDataset"/> <!-- Create Chart with passed props to filter chart-->
    </div>
  </div>
  </template>
  
  <script>
  import timeSeriesData from '../assets/data/timeseries.json';
  import Chart from './Chart.vue';
  import Table from './Table.vue';
  import VueDatePicker from '@vuepic/vue-datepicker';
  import '@vuepic/vue-datepicker/dist/main.css';
  
  export default {
    components: {
      Chart,
      Table,
      VueDatePicker
    },
    data() {
      return {
        date: null,
        Data: timeSeriesData,  // original time series data
        datasets: [
        { label: 'Germany', key: 'ENTSOE_DE_DAM_Price' },
        { label: 'Greece', key: 'ENTSOE_GR_DAM_Price' },
        { label: 'France', key: 'ENTSOE_FR_DAM_Price' }
      ],
      showDataset: {
        ENTSOE_DE_DAM_Price: true,
        ENTSOE_GR_DAM_Price: true,
        ENTSOE_FR_DAM_Price: true
      }
      };
    },
    computed: {
      filteredData() { //filter data based on the Date Range Picker
        if (!this.date) {
          return this.Data; // If no date range selected, return original data
        }
        
        const [startDate, endDate] = this.date;
        
        const startTimestamp = new Date(startDate).getTime();
        const endTimestamp = new Date(endDate).getTime();

        return this.Data.filter(entry => { //return filtered data
          const timestamp = new Date(entry.DateTime).getTime();
          return timestamp >= startTimestamp && timestamp <= endTimestamp;
        });
      }
  }
    
  };
  </script>
  