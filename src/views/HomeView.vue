<template>
  <Hero title="This is a title" subtitle="This is a subtitle" />
  <HomeCards />
  <JobsListings :limit="4" :showButton="true" />
</template>

<script setup>
import Hero from "../components/Hero.vue";
import HomeCards from "../components/HomeCards.vue";
import JobsListings from "@/components/JobsListings.vue";
</script>

<style></style>
