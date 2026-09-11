<script setup>
import { ref, onMounted, computed } from "vue";
import InputPlaceholder from "../components/InputPlaceholder.vue";
import TombolScrollUp from "../components/ScrollUpButton.vue";
import PilihanHari from "../components/PilihanHari.vue";
import DayWork from "../components/DayWork.vue";
import IconCopy from "../components/IconCopy.vue";

const JamLembur = ref("");
const GajiPokok = ref("");
const detailList = ref([]);
const total = ref("");
const kolekhasil = ref("");
const hasil2 = ref("");
const collectedResults = ref([]);
const boxCollected = ref([]);
const infoBagi = ref([]);
const totalCollected = ref(0);
const sembunyikan = ref(false);
const tampilkanHasil = ref(false);
const tmblUP = ref(false);
const errorKosong = ref(false);
const KosongBawah = ref(false);
const thisDay = ref("Day1");
const Day = ref("option1");
const hideWeekend = ref(false);
const ListPerhitungan = ref([]);

const handleScroll = () => {
  tmblUP.value = window.scrollY > 200;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});

const scrollHasil = () => {
  setTimeout(() => {
    document.getElementById("social").scrollIntoView({
      behavior: "smooth",
    });
  }, 100); // Delay untuk memastikan hasil sudah dirender
};

const scrollTotal = () => {
  setTimeout(() => {
    document.getElementById("koleksi-hasil").scrollIntoView({
      behavior: "smooth",
    });
  }, 100); // Delay untuk memastikan hasil sudah dirender
};

const tutupTooltip = () => {
  setTimeout(() => {
    errorKosong.value = false;
    KosongBawah.value = false;
  }, 5000); // Delay untuk menutup tooltip
};

const scrollHapus = () => {
  setTimeout(() => {
    document.getElementById("center").scrollIntoView({
      behavior: "smooth",
    });
  }, 100); // Delay untuk memastikan hasil sudah dirender
};

const TombolKeAtas = () => {
  window.scrollTo({
    top: 0,
    behavior: "smooth",
  });
};

// Format currency ke Rupiah
const formatRupiah = (number) => {
  return new Intl.NumberFormat("id-ID", {
    style: "currency",
    currency: "IDR",
    minimumFractionDigits: 0,
  }).format(number);
};

const hitung = () => {
  // Panggil HariygDipilih terlebih dahulu untuk setup ListPerhitungan
  HariygDipilih();

  if (GajiPokok.value === "" || GajiPokok.value === 0) {
    errorKosong.value = true;
    tutupTooltip();
    return;
  }
  if (JamLembur.value === "" || JamLembur.value === 0) {
    KosongBawah.value = true;
    errorKosong.value = false;
    tutupTooltip();
    return;
  }

  let upahPerjam = (1 / 173) * GajiPokok.value;
  detailList.value = []; // Reset detail
  let totalNilai = 0;
  const jamLemburCount = parseInt(JamLembur.value);

  // Hitung untuk setiap jam
  for (let jam = 1; jam <= jamLemburCount; jam++) {
    // Cari segment yang sesuai untuk jam ini
    const segment = ListPerhitungan.value.find(
      (item) => jam <= item.jam || item.jam === Infinity,
    );

    if (segment) {
      const nilai = upahPerjam * segment.kali;
      totalNilai += nilai;

      detailList.value.push({
        jam: jam,
        name: segment.name,
        kali: segment.kali,
        upahPerjam: formatRupiah(upahPerjam),
        hasil: nilai,
      });
    }
  }

  // Format dan display hasil
  total.value = formatRupiah(totalNilai);
  kolekhasil.value = `${formatRupiah(totalNilai)}`;
  hasil2.value = totalNilai;
  tampilkanHasil.value = true;
  scrollHasil();
};
const jumlahkanHasil = () => {
  if (hasil2.value !== "") {
    collectedResults.value.push(parseFloat(hasil2.value));
    boxCollected.value.push(parseFloat(GajiPokok.value));
    infoBagi.value.push({ JamLembur: JamLembur.value });
    totalCollected.value = collectedResults.value.reduce(
      (sum, val) => sum + val,
      0,
    );
  }
  sembunyikan.value = true;
  scrollTotal();
};

const copyNumber = async (value) => {
  try {
    await navigator.clipboard.writeText(String(value));
  } catch (error) {
    console.error("Gagal menyalin:", error);
  }
};

const HariygDipilih = () => {
  if (thisDay.value === "Day1") {
    ListPerhitungan.value = [
      { jam: 1, kali: 1.5, name: "Segmen 1" },
      { jam: 2, kali: 2, name: "Segmen 2" },
      { jam: Infinity, kali: 2, name: "Segmen 3" },
    ];
    hideWeekend.value = false;
  } else if (thisDay.value === "Day2") {
    ListPerhitungan.value = [
      { jam: 1, kali: 2, name: "Segmen 1" },
      { jam: 2, kali: 2, name: "Segmen 2" },
      { jam: 3, kali: 2, name: "Segmen 3" },
      { jam: 4, kali: 2, name: "Segmen 4" },
      { jam: 5, kali: 2, name: "Segmen 5" },
      { jam: 6, kali: 3, name: "Segmen 6" },
      { jam: 7, kali: 4, name: "Segmen 7" },
      { jam: 8, kali: 4, name: "Segmen 8" },
      { jam: 9, kali: 4, name: "Segmen 9" },
      { jam: 10, kali: 4, name: "Segmen 10" },
      { jam: Infinity, kali: 4, name: "Segmen 11" },
    ];
    hideWeekend.value = false;
  } else if (thisDay.value === "Day3") {
    hideWeekend.value = true;
    if (Day.value === "option1") {
      ListPerhitungan.value = [
        { jam: 1, kali: 2, name: "Segmen 1" },
        { jam: 2, kali: 2, name: "Segmen 2" },
        { jam: 3, kali: 2, name: "Segmen 3" },
        { jam: 4, kali: 2, name: "Segmen 4" },
        { jam: 5, kali: 2, name: "Segmen 5" },
        { jam: 6, kali: 2, name: "Segmen 6" },
        { jam: 7, kali: 2, name: "Segmen 7" },
        { jam: 8, kali: 2, name: "Segmen 8" },
        { jam: 9, kali: 3, name: "Segmen 9" },
        { jam: 10, kali: 4, name: "Segmen 10" },
        { jam: Infinity, kali: 4, name: "Segmen 11" },
      ];
    } else if (Day.value === "option2") {
      ListPerhitungan.value = [
        { jam: 1, kali: 2, name: "Segmen 1" },
        { jam: 2, kali: 2, name: "Segmen 2" },
        { jam: 3, kali: 2, name: "Segmen 3" },
        { jam: 4, kali: 2, name: "Segmen 4" },
        { jam: 5, kali: 2, name: "Segmen 5" },
        { jam: 6, kali: 2, name: "Segmen 6" },
        { jam: 7, kali: 2, name: "Segmen 7" },
        { jam: 8, kali: 3, name: "Segmen 8" },
        { jam: 9, kali: 4, name: "Segmen 9" },
        { jam: 10, kali: 4, name: "Segmen 10" },
        { jam: Infinity, kali: 4, name: "Segmen 11" },
      ];
    }
  }
};

//Hapus bagian Atas
const reset = () => {
  JamLembur.value = "";
  GajiPokok.value = "";
  detailList.value = [];
  total.value = "";
  kolekhasil.value = "";
  tampilkanHasil.value = false;
  scrollHapus();
};

// Hapus Toal bayaran yg dijumlahkan
const reset2 = () => {
  collectedResults.value = [];
  boxCollected.value = [];
  infoBagi.value = [];
  totalCollected.value = 0;
  sembunyikan.value = false;
};
</script>

<template>
  <TombolScrollUp v-if="tmblUP" @click="TombolKeAtas" class="btn-up" />
  <section id="center">
    <div id="atas">
      <h1>Kalkulator Lembur</h1>
    </div>
    <PilihanHari v-model="thisDay" @change="HariygDipilih" />
    <Transition name="fade">
      <div v-if="hideWeekend">
        <label>Pilih Hari Kerja:</label>
        <DayWork v-model="Day" />
      </div>
    </Transition>

    <div class="input-wrapper">
      <InputPlaceholder
        nama="Masukkan Gaji Pokok"
        v-model.number="GajiPokok"
        @keyup.enter="hitung"
      />
      <span v-if="errorKosong" class="tooltip"> Silahkan Diisi </span>
    </div>
    <div class="input-wrapper">
      <InputPlaceholder
        nama="Berapa Jam Lembur"
        v-model.number="JamLembur"
        @keyup.enter="hitung"
      />
      <span v-if="KosongBawah" class="tooltip"> Masih Kosong</span>
    </div>
    <button class="counter" @click="hitung">Hitung</button>
    <button class="klikhapus" @click="reset">Hapus</button>
  </section>

  <div class="ticks"></div>

  <section id="next-steps">
    <div v-if="tampilkanHasil" id="docs">
      <h2>Rincian Perhitungan</h2>
      <p>Gaji Pokok: {{ formatRupiah(GajiPokok) }}</p>
      <p>Upah Perjam: {{ formatRupiah((1 / 173) * GajiPokok) }}</p>
      <table id="detail-table">
        <tbody>
          <tr v-for="item in detailList" :key="item.jam">
            <td>Jam {{ item.jam }}</td>
            <td>:</td>
            <td>{{ item.upahPerjam }}</td>
            <td>x</td>
            <td>{{ item.kali }}</td>
            <td>=</td>
            <td>{{ formatRupiah(item.hasil) }}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <div v-if="tampilkanHasil" id="social">
      <h2>Hasil</h2>
      <h3 style="color: #72cf9f">{{ total }}</h3>
      <h2>Kumpulkan</h2>
      <button v-if="kolekhasil" class="counter" @click="jumlahkanHasil">
        {{ kolekhasil }}
      </button>
    </div>
  </section>

  <div class="ticks"></div>
  <section v-if="hasil2" id="koleksi-hasil">
    <h2>Upah Lembur yg dikumpulkan</h2>
    <table id="detail-table">
      <tbody>
        <tr v-for="(result, index) in collectedResults" :key="index">
          <td>Day {{ index + 1 }}</td>
          <td>:</td>
          <td>{{ infoBagi[index].JamLembur }} Jam Lembur</td>
          <td>|</td>
          <td>{{ formatRupiah(result) }}</td>
        </tr>
      </tbody>
    </table>

    <p>===============================</p>
    <p>Total Upah Lembur:</p>
    <div class="number-copy">
      <span style="color: #72cf9f; font-size: 1.5em; font-weight: bold">
        {{ formatRupiah(totalCollected) }}
      </span>
      <IconCopy
        v-if="totalCollected"
        @click="copyNumber(formatRupiah(totalCollected))"
      />
    </div>
    <section id="spacer"></section>
    <button v-if="sembunyikan" class="klikhapus" @click="reset2">
      Bersihkan Total Upah Lembur
    </button>
  </section>

  <div class="ticks"></div>
  <section id="spacer"></section>
</template>
