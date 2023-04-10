<template>
  <Navbar />
  <div class="container">
    <div class="row">
      <div class="col">
        <CountriesList />
      </div>
      <div class="col">
        <CountryDetails />
      </div>
    </div>
  </div>
</template>

<script setup>
  import Navbar from './components/Navbar.vue';
  import CountriesList from './components/CountriesList.vue';
  import CountryDetails from './components/CountryDetails.vue';
</script>

<style>

</style>