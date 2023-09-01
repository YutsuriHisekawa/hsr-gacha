<script setup>
import { ref } from 'vue';
//SSR
import SeeleImage from '../assets/images/ssr/Seele.png';
import BronyaImage from '../assets/images/ssr/Bronya.png';
import SilverImage from '../assets/images/ssr/Silverwolf.png';
//SR
import TingyunImage from '../assets/images/sr/Tingyun.png';
//R
import BatuImage from '../assets/images/r/Batu.png';

const SSR = [
  { name: 'Seele', image: SeeleImage },
  { name: 'Bronya', image: BronyaImage },
  { name: 'Silverwolf', image: SilverImage },
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

const rollOnce = () => {
  const random = Math.random() * 100;
  if (random < 5) {
    return SSR[Math.floor(Math.random() * SSR.length)];
  } else if (random < 22) {
    return SR[Math.floor(Math.random() * SR.length)];
  } else {
    return R[Math.floor(Math.random() * R.length)];
  }
};

const rollGacha = () => {
  results.value = [rollOnce()];
};

const rollGacha10x = () => {
  results.value = Array.from({ length: 10 }, () => rollOnce());
};

const results = ref([]);

const resetGacha = () => {
  results.value = [];
};
</script>

<template>
  <div class="p-4">
    <div class="flex justify-center mb-4">
      <button
        @click="rollGacha"
        class="bg-blue-500 hover:bg-blue-600 dark:bg-gray-200 dark:hover:bg-slate-300 duration-300 rounded-xl dark:text-black text-white p-4 m-2 font-semibold">
        Roll Gacha 1x
      </button>
      <button
        @click="rollGacha10x"
        class="bg-green-500 hover:bg-green-600 rounded-xl text-white p-4 m-2">
        Roll Gacha 10x
      </button>
      <button
        @click="resetGacha"
        class="bg-red-500 hover:bg-red-600 rounded-xl text-white p-4 m-2">
        Reset Gacha
      </button>
    </div>
    <div
      v-if="results.length"
      class="grid grid-cols-2 md:grid-cols-4 gap-4 mt-4 flex justify-center">
      <div
        v-for="(result, index) in results"
        :key="index"
        :class="results.length === 1 ? 'col-span-2 md:col-span-4' : 'col-span-1'">
        <img
          :src="result.image"
          :alt="result.name"
          class="mx-auto" />
        <h2 class="text-center mt-2 font-bold dark:text-white">{{ result.name }}</h2>
      </div>
    </div>
  </div>
</template>
