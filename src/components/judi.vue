<script setup>
import { ref } from 'vue';
//SSR
import SeeleImage from '../assets/images/ssr/Seele.png';
import BronyaImage from '../assets/images/ssr/Bronya.png';
import SilverImage from '../assets/images/ssr/Silverwolf.png';
import BailuImage from '../assets/images/ssr/Bailu.png';
import BladeImage from '../assets/images/ssr/Blade.webp';
import ClaraImage from '../assets/images/ssr/Clara.png';
import GepardImage from '../assets/images/ssr/Gepard.png';
import HimekoImage from '../assets/images/ssr/Himeko.png';
import JingYuanImage from '../assets/images/ssr/JingYuan.webp';
import KafkaImage from '../assets/images/ssr/Kafka.png';
import LuochaImage from '../assets/images/ssr/Luocha.png';
import WeltImage from '../assets/images/ssr/Welt.png';
import YanqingImage from '../assets/images/ssr/Yanqing.png';
//SR
import TingyunImage from '../assets/images/sr/Tingyun.png';
import DanhengImage from '../assets/images/sr/Danheng.png';
import SushangImage from '../assets/images/sr/Sushang.png';
import ServalImage from '../assets/images/sr/Serval.png';
import ArlanImage from '../assets/images/sr/Arlan.png';
import AstaImage from '../assets/images/sr/Asta.png';
import HertaImage from '../assets/images/sr/Herta.png';
import HookImage from '../assets/images/sr/Hook.png';
import March7thImage from '../assets/images/sr/March7th.png';
import NatashaImage from '../assets/images/sr/Natasha.png';
import PelaImage from '../assets/images/sr/Pela.png';
import QingqueImage from '../assets/images/sr/Qingque.png';
import SampoImage from '../assets/images/sr/Sampo.png';
//R
import BatuImage from '../assets/images/r/Batu.png';

const SSR = [
  { name: 'Seele', image: SeeleImage },
  { name: 'Bronya', image: BronyaImage },
  { name: 'Silverwolf', image: SilverImage },
  { name: 'Bailu', image: BailuImage },
  { name: 'Blade', image: BladeImage },
  { name: 'Clara', image: ClaraImage },
  { name: 'Gepard', image: GepardImage },
  { name: 'Himeko', image: HimekoImage },
  { name: 'Jing Yuan', image: JingYuanImage },
  { name: 'Kafka', image: KafkaImage },
  { name: 'Luocha', image: LuochaImage },
  { name: 'Welt', image: WeltImage },
  { name: 'Yanqing', image: YanqingImage },
];
const R = [{ name: 'Batu', image: BatuImage }];
const SR = [
  { name: 'Tingyun', image: TingyunImage },
  { name: 'Danheng', image: DanhengImage },
  { name: 'Sushang', image: SushangImage },
  { name: 'Serval', image: ServalImage },
  { name: 'Arlan', image: ArlanImage },
  { name: 'Asta', image: AstaImage },
  { name: 'Herta', image: HertaImage },
  { name: 'Hook', image: HookImage },
  { name: 'March 7th', image: March7thImage },
  { name: 'Natasha', image: NatashaImage },
  { name: 'Pela', image: PelaImage },
  { name: 'Qingque', image: QingqueImage },
  { name: 'Sampo', image: SampoImage },
];

// Variabel untuk menentukan apakah popup harus ditampilkan
const showSSRPopup = ref(false);
const ssrResult = ref(null);
const ssrCounter = ref(0);
const loading = ref(false);
const results = ref([]);

const rollOnce = () => {
  const random = Math.random() * 100; // ini akan memberi kita angka antara 0 dan 100
  let result;

  if (random < 0.8 || ssrCounter.value >= 80) {
    // Cek apakah angka acak kurang dari 0.8 (0.80%)
    result = SSR[Math.floor(Math.random() * SSR.length)];
    ssrCounter.value = 0; // reset counter jika mendapatkan SSR
    ssrResult.value = result;
    showSSRPopup.value = true;
  } else if (random < 20) {
    // Anda mungkin perlu menyesuaikan angka ini tergantung pada rate lain yang Anda inginkan
    result = SR[Math.floor(Math.random() * SR.length)];
    ssrCounter.value++; // increment counter
  } else {
    result = R[Math.floor(Math.random() * R.length)];
    ssrCounter.value++; // increment counter
  }
  return result;
};

const rollGacha10x = async () => {
  loading.value = true;
  let tempResults = Array.from({ length: 9 }, rollOnce);
  let hasSR = tempResults.some((result) => SR.includes(result));
  if (!hasSR || ssrCounter.value >= 80) tempResults.push(SR[Math.floor(Math.random() * SR.length)]);
  else tempResults.push(rollOnce());
  results.value = tempResults;
  await new Promise((r) => setTimeout(r, 10000));
  loading.value = false;
};

const rollGacha = async () => {
  loading.value = true;
  results.value = [rollOnce()];
  await new Promise((r) => setTimeout(r, 1000));
  loading.value = false;
};

const resetGacha = () => {
  results.value = [];
};

const closeSSRPopup = () => {
  showSSRPopup.value = false;
};
</script>

<template>
  <div class="p-4 relative">
    <!-- relative untuk posisi popup -->
    <!-- Jika sedang loading -->
    <div
      v-if="loading"
      class="flex justify-center my-5">
      <div class="loader"></div>
    </div>

    <!-- Tombol-tombol aksi -->
    <div class="flex justify-center mb-4">
      <button
        @click="rollGacha"
        class="bg-gray-400 hover:bg-gray-500 mr-4 p-4 font-bold text-white duration-300 rounded-2xl">
        Roll Gacha 1x
      </button>
      <button
        @click="rollGacha10x"
        class="bg-lime-500 hover:bg-green-600 mr-4 p-4 font-bold text-white duration-300 rounded-2xl">
        Roll Gacha 10x
      </button>
      <button
        @click="resetGacha"
        class="bg-red-500 hover:bg-red-600 mr-4 p-4 font-bold text-white duration-300 rounded-2xl">
        Reset Gacha
      </button>
    </div>

    <!-- Hasil roll -->
    <!-- Jika hanya ada 1 hasil -->
    <div
      v-if="results.length === 1"
      class="flex justify-center mt-4">
      <div>
        <img
          :src="results[0].image"
          :alt="results[0].name"
          class="mx-auto w-1/2" />
        <h2 class="text-center mt-2 font-bold dark:text-white">{{ results[0].name }}</h2>
      </div>
    </div>

    <!-- Jika ada lebih dari 1 hasil -->
    <div
      v-else-if="results.length > 1"
      class="grid grid-cols-3 md:grid-cols-5 gap-4 mt-4">
      <div
        v-for="(result, index) in results"
        :key="index">
        <img
          :src="result.image"
          :alt="result.name" />
        <h2 class="text-center mt-2 font-bold dark:text-white">{{ result.name }}</h2>
      </div>
    </div>

    <!-- Popup SSR -->
    <div
      v-if="showSSRPopup"
      class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50"
      @click="closeSSRPopup">
      <!-- Menambahkan @click untuk menutup popup ketika div ini diklik -->
      <img
        :src="ssrResult.image"
        :alt="ssrResult.name"
        @click.stop="closeSSRPopup"
        class="w-1/2 cursor-pointer" />
    </div>
  </div>
</template>
