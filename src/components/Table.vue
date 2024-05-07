<template>

<div class=" max-h-96 relative overflow-x-auto sm:rounded py-10 pt-0">
    <table class="w-full h-100 text-sm text-left rtl:text-right text-gray-500">
        <thead class="text-xs text-gray-700 uppercase bg-gray-100">
            <tr>
                <th scope="col" class="px-6 py-3">
                    Timestamp
                </th>
                <th v-for="(dataset, key) in filteredDatasets" :key="key">{{ dataset.label }}</th> <!--Create dynamic table heads based on the filteredDatasets / Show the label from the dataset prop passed from the parent component-->
            </tr>
        </thead>
        <tbody>
            <tr v-for="timeData in filteredData" :key="timeData.DateTime" class="bg-white border-b"> <!--Create dynamic table rows based on the filteredData from parent component-->
                <td class="px-6 py-4">{{ formatDate(timeData.DateTime) }}</td> <!-- Show the formated date from the filteredData-->
                <td v-for="(dataset, key) in filteredDatasets" :key="key">{{ timeData[dataset.key] }}</td> <!-- Show the filtered data for each dataset in the filteredDatasets-->
            </tr>
        </tbody>
    </table>
</div>

  </template>
  
  <script>


  export default {
    props:['filteredData', 'showDataset', 'datasets'],
    computed: {
        filteredDatasets() { //filter the datasets set based on the showDataset prop passed from the parent component
        return this.datasets.filter(dataset => this.showDataset[dataset.key]);
        }
    },
    methods: {
        formatDate(dateTime) { //format the iso date to en-US
            return new Date(dateTime).toLocaleString('en-US', { dateStyle: 'medium', timeStyle: 'short' });
        } 
    }
  };

  </script>
  
