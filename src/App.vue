<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100">
    <div class="p-4 bg-white rounded shadow-lg max-w-lg w-full">
      <Gacha />
    </div>
  </div>
</template>

<script>
import Gacha from './components/Gacha.vue';

export default {
  components: {
    Gacha,
  },
};
</script>

<style>
/* Anda bisa menambahkan styling global disini jika perlu */
</style>
