<template>
  <div class="home">
    <ProgressBar />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import ProgressBar from '@/components/ProgressBar.vue'; // @ is an alias to /src

export default Vue.extend({
  name: 'HomeView',
  components: {
    ProgressBar,
  },
});
</script>

<style scoped>
  
</style>
