<script setup>
import { ref } from 'vue';
import SeeleImage from '../assets/images/ssr/Seele.png';
import BronyaImage from '../assets/images/ssr/Bronya.png';
import BatuImage from '../assets/images/r/Batu.png';
import TingyunImage from '../assets/images/sr/Tingyun.png';

const SSR = [
  { name: 'Seele', image: SeeleImage },
  { name: 'Bronya', image: BronyaImage },
  // ... (complete all SSR characters)
];
const R = [
  { name: 'Batu', image: BatuImage },
  // ... (complete all R characters)
];

const SR = [
  { name: 'Tingyun', image: TingyunImage },
  // ... (complete all SR characters)
];

const rollGacha = () => {
  const random = Math.random() * 100;
  if (random < 2) {
    result.value = SSR[Math.floor(Math.random() * SSR.length)];
  } else if (random < 22) {
    result.value = SR[Math.floor(Math.random() * SR.length)];
  } else {
    result.value = R[Math.floor(Math.random() * R.length)];
  }
};

const result = ref(null);
</script>

<template>
  <div>
    <button
      @click="rollGacha"
      class="bg-blue-500 text-white p-4">
      Roll Gacha 1x
    </button>
    <div v-if="result">
      <img
        :src="result.image"
        :alt="result.name"
        class="max-w-xs mx-auto my-4" />
      <h2 class="text-center">{{ result.name }}</h2>
    </div>
  </div>
</template>
