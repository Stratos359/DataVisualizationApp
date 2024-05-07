<h1>Timeseries Data Visualization App</h1>

<h2>Features</h2>

<ul>
  <li>Display timeseries data in a table</li>
  <li>Visualize timeseries data with an interactive chart</li>
  <li>Filter data by date range</li>
  <li>Toggle visibility of datasets with checkboxes</li>
</ul>

<h2>Installation</h2>

<ol>
  <li>Clone the repository:</li>
  <code>git clone https://github.com/Stratos359/DataVisualizationApp.git</code>
  <li>Navigate to the project directory:</li>
  <code>cd DataVisualizationApp</code>
  <li>Install dependencies:</li>
  <code>npm install</code>
  <li>Run the development server:</li>
  <code>npm run serve</code>
  <li>Open your browser and navigate to <a href="http://localhost:8080">http://localhost:8080</a> to view the application.</li>
</ol>

<h2>Usage</h2>

<ol>
  <li>Select date range using the date picker to filter data.</li>
  <li>Toggle checkboxes to show/hide datasets on the table and chart.</li>
  <li>Explore the chart and table to analyze timeseries data.</li>
</ol>

<h2>Technologies Used</h2>

<ul>
  <li>Vue.js: JavaScript framework for building user interfaces</li>
  <li>Flowbite Vue: Vue.js UI framework for building responsive web interfaces</li>
  <li>Chart.js: JavaScript charting library for creating interactive charts</li>
  <li>Vue Datepicker: Vue.js datepicker component for selecting date ranges</li>
</ul>

<h2>Project Structure</h2>

<p>The project is organized into the following directories:</p>
<ul>
  <li><code>src/App.vue</code>: Main Vue component that serves as the entry point of the application.</li>
  <li><code>main.js</code>: JavaScript file that initializes the Vue application and mounts it to the DOM.</li>
  <li><code>src/components</code>: Contains Vue components for different parts of the application.</li>
  <ul>
    <li><code>DataVisualization.vue</code>: Vue component serving as the parent/container component that encapsulates the other components and manages the overall state of the application.</li>
    <li><code>Chart.vue</code>: Vue component responsible for rendering the interactive chart using Chart.js. It receives filtered data and dataset visibility as props and updates the chart accordingly.</li>
    <li><code>Table.vue</code>: Vue component responsible for displaying timeseries data in a table format. It receives filtered data and dataset visibility as props and dynamically renders the table rows and columns.</li>
    <li><code>DateRangePicker.vue</code>: Vue component for selecting date ranges using Vue Datepicker. It emits events when the date range changes, allowing the parent component to update the filtered data accordingly.</li>
    <li><code>Navbar.vue</code>: Vue component representing the navigation bar of the application.</li>
    <li><code>Footer.vue</code>: Vue component representing the footer section of the application.</li>
  </ul>
  <li><code>src/assets/data</code>: Contains the timeseries.json file </li>
</ul>

<p>Each component is responsible for a specific part of the application's user interface and functionality. They are designed to be reusable and modular, allowing for easy integration and customization within the application.</p>

