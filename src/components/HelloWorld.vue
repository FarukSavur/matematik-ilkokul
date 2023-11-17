<script setup></script>

<template>
  <div class="container mx-auto">
    <h1 class="text-6xl font-serif text-center p-5">Matematik Uygulaması</h1>
    <div
      class="flex items-center justify-evenly gap-3 p-3 border-4 border-slate-500 rounded-2xl shadow-2xl bg-slate-200"
    >
      <div class="fixed z-10" :class="{ 'inset-0 ': kilitle }"></div>
      <div
        class="bg-slate-400 flex flex-col flex-1 p-5 rounded-2xl text-center relative"
        :class="birinci_kullanici[0].dogruYanit == '' ? 'bg-red-700' : 'bg-blue-400'"
      >
        <div class="absolute top-2 right-2 bg-green-600 px-2 py-1 rounded-lg font-mono">
          Puan: {{ this.birinci_kullanici[0].puan }}
        </div>
        <div class="flex items-center justify-center gap-2 text-3xl text-red-700">
          <i class="fa-solid fa-heart" v-for="i in birinci_kullanici[0].can"></i>
        </div>

        <div
          class="absolute top-2 left-2 bg-blue-600 px-2 py-1 rounded-lg font-mono"
          v-if="birinci_kullanici[0].dogruYanit"
        >
          Doğru cevap
        </div>
        <h1 class="text-4xl mt-1 font-mono">{{ sorular[aktifSoruIndex].soru }}</h1>
        <div class="flex items-center justify-evenly gap-5 mt-4">
          <div
            class="w-24 h-14 flex items-center justify-center text-3xl font-mono bg-slate-500 rounded-lg shadow-xl cursor-pointer"
            v-for="(cevap, index) in sorular[aktifSoruIndex].cevaplar"
            :key="index"
            @click="writeAnswer(cevap, 1)"
          >
            {{ cevap }}
          </div>
        </div>
      </div>
      <div
        class="bg-slate-400 flex flex-col flex-1 p-5 rounded-2xl text-center relative"
        :class="ikinci_kullanici[0].dogruYanit == '' ? 'bg-red-700' : ''"
      >
        <div class="absolute top-2 right-2 bg-green-600 px-2 py-1 rounded-lg font-mono">
          Puan: {{ this.ikinci_kullanici[0].puan }}
        </div>
        <div class="flex items-center justify-center gap-2 text-3xl text-red-700">
          <i class="fa-solid fa-heart" v-for="i in ikinci_kullanici[0].can"></i>
        </div>
        <div
          class="absolute top-2 left-2 bg-blue-600 px-2 py-1 rounded-lg font-mono"
          v-if="ikinci_kullanici[0].dogruYanit"
        >
          Doğru cevap
        </div>
        <h1 class="text-4xl mt-1 font-mono">{{ sorular[aktifSoruIndex].soru }}</h1>
        <div class="flex items-center justify-evenly gap-5 mt-4">
          <div
            class="w-24 h-14 flex items-center justify-center text-3xl font-mono bg-slate-500 rounded-lg shadow-xl cursor-pointer"
            v-for="(cevap, index) in sorular[aktifSoruIndex].cevaplar"
            :key="index"
            @click="writeAnswer(cevap, 2)"
          >
            {{ cevap }}
          </div>
        </div>
      </div>
    </div>
    <div class="w-full flex justify-between mt-3">
      <!-- <button
        class="bg-blue-500 text-white font-bold py-2 px-4 rounded"
        :class="aktifSoruIndex == 0 ? 'bg-red-700' : ''"
        @click="
          () => {
            if (aktifSoruIndex != 0) {
              aktifSoruIndex--;
            }
          }
        "
      >
        Geri
      </button>
      {{ sorular.length - 1 + " ----- " + aktifSoruIndex }}

      <button
        class="bg-blue-500 text-white font-bold py-2 px-4 rounded"
        :class="sorular.length - 1 == aktifSoruIndex ? 'bg-red-700' : ''"
        @click="
          () => {
            if (sorular.length - 1 > aktifSoruIndex) {
              aktifSoruIndex++;
            }
          }
        "
      >
        İleri
      </button> -->
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      aktifSoruIndex: 0,
      birinci_kullanici: [
        {
          can: 3,
          puan: 0,
          dogruYanit: "",
        },
      ],
      ikinci_kullanici: [
        {
          can: 3,
          puan: 0,
          dogruYanit: "",
        },
      ],
      // kilitle: false,
      kilitle: false,
      sorular: [
        {
          soru: "3 x 5 = ?",
          cevaplar: ["8", "12", "15", "20"],
          dogruCevap: "15",
        },
        {
          soru: "7 + 2 = ?",
          cevaplar: ["8", "9", "10", "11"],
          dogruCevap: "9",
        },
        {
          soru: "6 / 2 = ?",
          cevaplar: ["2", "3", "4", "5"],
          dogruCevap: "3",
        },
        {
          soru: "4 - 1 = ?",
          cevaplar: ["2", "3", "4", "5"],
          dogruCevap: "3",
        },
        {
          soru: "9 x 4 = ?",
          cevaplar: ["32", "36", "40", "45"],
          dogruCevap: "36",
        },
        {
          soru: "12 / 3 = ?",
          cevaplar: ["2", "3", "4", "6"],
          dogruCevap: "4",
        },
        {
          soru: "5 + 8 = ?",
          cevaplar: ["10", "12", "13", "14"],
          dogruCevap: "13",
        },
        {
          soru: "10 - 7 = ?",
          cevaplar: ["1", "2", "3", "4"],
          dogruCevap: "3",
        },
        {
          soru: "2 x 9 = ?",
          cevaplar: ["14", "16", "18", "20"],
          dogruCevap: "18",
        },
        {
          soru: "15 / 5 = ?",
          cevaplar: ["2", "3", "4", "5"],
          dogruCevap: "3",
        },
      ],
    };
  },
  methods: {
    writeAnswer(cevap, kullanici_id) {
      // let soru = this.sorular[this.aktifSoruIndex].soru;
      let dogruCevap = this.sorular[this.aktifSoruIndex].dogruCevap;
      if (dogruCevap == cevap) {
        this.kilitle = true;

        setTimeout(() => {
          this.aktifSoruIndex++;
          this.kilitle = false;
          this.birinci_kullanici[0].dogruYanit = false;
          this.ikinci_kullanici[0].dogruYanit = false;
        }, 1000);
        if (kullanici_id == 1) {
          this.birinci_kullanici[0].dogruYanit = true;
          this.birinci_kullanici[0].puan += 1;
        }
        if (kullanici_id == 2) {
          this.ikinci_kullanici[0].dogruYanit = true;
          this.ikinci_kullanici[0].puan += 1;
        }
      } else {
        if (kullanici_id == 1) {
          this.birinci_kullanici[0].dogruYanit = false;
          this.birinci_kullanici[0].can--;
        }
        if (kullanici_id == 2) {
          this.ikinci_kullanici[0].can--;
          this.ikinci_kullanici[0].dogruYanit = false;
        }
      }
    },
  },
};
</script>
