<script setup>
import judi from './components/judi.vue';
import bar from './components/bar.vue';
</script>

<template>
  <bar />
  <div
    class="min-h-screen w-full flex items-center justify-center bg-gray-100 dark:bg-gray-950 pt-36 pb-36">
    <div
      class="p-4 ml-5 mr-5 bg-white dark:bg-gray-600 rounded shadow-lg max-w-3xl w-full mt-5 mb-5">
      <judi></judi>
    </div>
  </div>
</template>
