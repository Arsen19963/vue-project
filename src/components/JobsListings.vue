<template>
  <section class="bg-blue-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-6" v-else>
        <JobListing
          v-for="job in state.jobs.slice(0, limit || state.jobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>
  <section class="m-auto max-w-lg my-10 px-6" v-if="showButton">
    <RouterLink
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>

<script setup>
import { reactive, onMounted } from "vue";
import JobListing from "./JobListing.vue";
import { RouterLink } from "vue-router";
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

const state = reactive({
  jobs: [],
  isLoading: true,
});

function delay(ms) {
  return new Promise((resolve) => setTimeout(resolve, ms));
}

onMounted(async () => {
  try {
    const [response] = await Promise.all([axios.get("/api/jobs"), delay(100)]);
    state.jobs = response.data;
  } catch (error) {
    console.error("Error getting jobs", error);
  } finally {
    state.isLoading = false;
  }
});

defineProps({
  limit: Number,
  showButton: { type: Boolean, default: false },
});
</script>

<style></style>
