<script setup>
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import HomeCards from "./components/HomeCards.vue";
import JobListings from "./components/JobListings.vue";
</script>

<template id="app">
  <Navbar />
  <Hero />
  <HomeCards />
  <JobListings :limit="2" :showButton="true" />
</template>
