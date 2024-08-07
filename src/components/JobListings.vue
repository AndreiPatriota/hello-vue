<script setup>
  import { ref, onMounted, reactive } from 'vue';
  // import jobData from '../jobs.json';
  import JobListing from './JobListing.vue';
  import axios from 'axios';
  import { RouterLink } from 'vue-router';
  import PulseLoader from 'vue-spinner/src/PulseLoader.vue';

  const state = reactive({ jobs: [], isLoading: true });

  const props = defineProps({
    limit: {
      type: Number,
    },
    showButton: {
      type: Boolean,
      default: false,
    },
  });

  onMounted(async () => {
    try {
      const response = await axios.get('/api/jobs');
      state.jobs = response.data;
    } catch (error) {
      console.error(`Error while fecthing jobs: ${error}`);
    } finally {
      state.isLoading = false;
    }
  });
</script>

<template>
  <section class="bg-green-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <!-- Show loading spinner -->
      <div v-if="state.isLoading" class="text-center text-gray-500 py-6">
        <PulseLoader />
      </div>
      <!-- Show list of jobs after loading -->
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <JobListing
          v-for="job in state.jobs.slice(0, props.limit || state.jobs.length)"
          :key="job.id"
          :job="job" />
      </div>
    </div>
  </section>

  <section class="m-auto max-w-lg my-10 px-6" v-show="props.showButton">
    <RouterLink
      to="/jobs/"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs
    </RouterLink>
  </section>
</template>
