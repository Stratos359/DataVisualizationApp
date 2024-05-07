<template>
  <Navbar/>
  <DataVisualization/>
  <Footer/>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Footer from './components/Footer.vue';
import DataVisualization from './components/DataVisualization.vue';

export default {
  name: 'App',
  components: {
    Navbar,
    Footer,
    DataVisualization
  }
}
</script>

<style>

</style>
