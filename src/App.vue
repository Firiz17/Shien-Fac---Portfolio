<script setup>
import {ref} from 'vue'

// creates an empty reactive list
const prayerTimes = ref([]);

const zone = ref('JHR01');
const period = ref('today');
const isLoading = ref(false);
/**
 * Fetches prayer times from e-solat.gov.my API based on specified period and zone
 * @param {string} period - Time period (e.g., 'day', 'week', 'month')
 * @param {string} zone - Location zone code (e.g., 'SGR01', 'PNG01')
 * @returns {Promise<void>}
 */
async function LoadPrayerTimes(period, zone) {
  isLoading.value = true
  // Make an HTTP GET request to the e-solat API with period and zone parameters
  let response = await fetch(`https://www.e-solat.gov.my/index.php?r=esolatApi/TakwimSolat&period=${period}&zone=${zone}`)

  // Parse the response body from JSON format to a JavaScript object
  let jsonData = (await response.json())

  // Artificial delay of 1.5 seconds
  await new Promise(resolve => setTimeout(resolve, 1500))
  // Extract the prayer times array from the response data and update the reactive reference
  // This will trigger any UI components that depend on prayerTimes to re-render
  prayerTimes.value = jsonData.prayerTime

  isLoading.value = false  // End loading state


}

</script>

<template>
<div class="min-h-screen flex flex-col ">
  <div class="container mx-auto my-5">
    <div class="flex outline-none items-center justify-between">
      <h1 class="text-2xl font-bold my-4 font ">Prayer Times with Vue JS and TailwindCSS</h1>
      <select v-model="period" class="ml-2 w-1/6 outline-none rounded-lg px-1 py-1 shadow-sm ">
        <option selected value="today">Today</option>
        <option value="week">This Week</option>
        <option value="month">This Month</option>
        <option value="year">This Year</option>
      </select>
    </div>
    <div class="flex flex-col ">
      <select v-model="zone" id="inputzone" class="px-2 py-3 rounded-md bg-gray-50 border border-zinc-200 focus:outline-none active:border-white shadow">
        <option selected="">Tukar Zon..</option>
        <optgroup label="Johor">
          <option value="JHR01" class="hs">JHR01 - Pulau Aur dan Pulau Pemanggil</option>
          <option value="JHR02" class="hs">JHR02 - Johor Bahru, Kota Tinggi, Mersing, Kulai</option>
          <option value="JHR03" class="hs">JHR03 - Kluang, Pontian</option>
          <option value="JHR04" class="hs">JHR04 - Batu Pahat, Muar, Segamat, Gemas Johor, Tangkak</option>
        </optgroup>
        <optgroup label="Kedah">
          <option value="KDH01" class="hs">KDH01 - Kota Setar, Kubang Pasu, Pokok Sena (Daerah Kecil)</option>
          <option value="KDH02" class="hs">KDH02 - Kuala Muda, Yan, Pendang</option>
          <option value="KDH03" class="hs">KDH03 - Padang Terap, Sik</option>
          <option value="KDH04" class="hs">KDH04 - Baling</option>
          <option value="KDH05" class="hs">KDH05 - Bandar Baharu, Kulim</option>
          <option value="KDH06" class="hs">KDH06 - Langkawi</option>
          <option value="KDH07" class="hs">KDH07 - Puncak Gunung Jerai</option>
        </optgroup>
        <optgroup label="Kelantan">
          <option value="KTN01" class="hs">KTN01 - Bachok, Kota Bharu, Machang, Pasir Mas, Pasir Puteh, Tanah Merah,
            Tumpat, Kuala Krai, Mukim Chiku
          </option>
          <option value="KTN02" class="hs">KTN02 - Gua Musang (Daerah Galas Dan Bertam), Jeli, Jajahan Kecil Lojing
          </option>
        </optgroup>
        <optgroup label="Melaka">
          <option value="MLK01" class="hs">MLK01 - SELURUH NEGERI MELAKA</option>
        </optgroup>
        <optgroup label="Negeri Sembilan">
          <option value="NGS01" class="hs">NGS01 - Tampin, Jempol</option>
          <option value="NGS02" class="hs">NGS02 - Jelebu, Kuala Pilah, Rembau</option>
          <option value="NGS03" class="hs">NGS03 - Port Dickson, Seremban</option>
        </optgroup>
        <optgroup label="Pahang">
          <option value="PHG01" class="hs">PHG01 - Pulau Tioman</option>
          <option value="PHG02" class="hs">PHG02 - Kuantan, Pekan, Rompin, Muadzam Shah</option>
          <option value="PHG03" class="hs">PHG03 - Jerantut, Temerloh, Maran, Bera, Chenor, Jengka</option>
          <option value="PHG04" class="hs">PHG04 - Bentong, Lipis, Raub</option>
          <option value="PHG05" class="hs">PHG05 - Genting Sempah, Janda Baik, Bukit Tinggi</option>
          <option value="PHG06" class="hs">PHG06 - Cameron Highlands, Genting Higlands, Bukit Fraser</option>
        </optgroup>
        <optgroup label="Perlis">
          <option value="PLS01" class="hs">PLS01 - Kangar, Padang Besar, Arau</option>
        </optgroup>
        <optgroup label="Pulau Pinang">
          <option value="PNG01" class="hs">PNG01 - Seluruh Negeri Pulau Pinang</option>
        </optgroup>
        <optgroup label="Perak">
          <option value="PRK01" class="hs">PRK01 - Tapah, Slim River, Tanjung Malim</option>
          <option value="PRK02" class="hs">PRK02 - Kuala Kangsar, Sg. Siput , Ipoh, Batu Gajah, Kampar</option>
          <option value="PRK03" class="hs">PRK03 - Lenggong, Pengkalan Hulu, Grik</option>
          <option value="PRK04" class="hs">PRK04 - Temengor, Belum</option>
          <option value="PRK05" class="hs">PRK05 - Kg Gajah, Teluk Intan, Bagan Datuk, Seri Iskandar, Beruas, Parit,
            Lumut, Sitiawan, Pulau Pangkor
          </option>
          <option value="PRK06" class="hs">PRK06 - Selama, Taiping, Bagan Serai, Parit Buntar</option>
          <option value="PRK07" class="hs">PRK07 - Bukit Larut</option>
        </optgroup>
        <optgroup label="Sabah">
          <option value="SBH01" class="hs">SBH01 - Bahagian Sandakan (Timur), Bukit Garam, Semawang, Temanggong,
            Tambisan, Bandar Sandakan, Sukau
          </option>
          <option value="SBH02" class="hs">SBH02 - Beluran, Telupid, Pinangah, Terusan, Kuamut, Bahagian Sandakan
            (Barat)
          </option>
          <option value="SBH03" class="hs">SBH03 - Lahad Datu, Silabukan, Kunak, Sahabat, Semporna, Tungku, Bahagian
            Tawau (Timur)
          </option>
          <option value="SBH04" class="hs">SBH04 - Bandar Tawau, Balong, Merotai, Kalabakan, Bahagian Tawau (Barat)
          </option>
          <option value="SBH05" class="hs">SBH05 - Kudat, Kota Marudu, Pitas, Pulau Banggi, Bahagian Kudat</option>
          <option value="SBH06" class="hs">SBH06 - Gunung Kinabalu</option>
          <option value="SBH07" class="hs">SBH07 - Kota Kinabalu, Ranau, Kota Belud, Tuaran, Penampang, Papar, Putatan,
            Bahagian Pantai Barat
          </option>
          <option value="SBH08" class="hs">SBH08 - Pensiangan, Keningau, Tambunan, Nabawan, Bahagian Pendalaman (Atas)
          </option>
          <option value="SBH09" class="hs">SBH09 - Beaufort, Kuala Penyu, Sipitang, Tenom, Long Pasia, Membakut, Weston,
            Bahagian Pendalaman (Bawah)
          </option>
        </optgroup>
        <optgroup label="Selangor">
          <option value="SGR01" class="hs">SGR01 - Gombak, Petaling, Sepang, Hulu Langat, Hulu Selangor, S.Alam</option>
          <option value="SGR02" class="hs">SGR02 - Kuala Selangor, Sabak Bernam</option>
          <option value="SGR03" class="hs">SGR03 - Klang, Kuala Langat</option>
        </optgroup>
        <optgroup label="Sarawak">
          <option value="SWK01" class="hs">SWK01 - Limbang, Lawas, Sundar, Trusan</option>
          <option value="SWK02" class="hs">SWK02 - Miri, Niah, Bekenu, Sibuti, Marudi</option>
          <option value="SWK03" class="hs">SWK03 - Pandan, Belaga, Suai, Tatau, Sebauh, Bintulu</option>
          <option value="SWK04" class="hs">SWK04 - Sibu, Mukah, Dalat, Song, Igan, Oya, Balingian, Kanowit, Kapit
          </option>
          <option value="SWK05" class="hs">SWK05 - Sarikei, Matu, Julau, Rajang, Daro, Bintangor, Belawai</option>
          <option value="SWK06" class="hs">SWK06 - Lubok Antu, Sri Aman, Roban, Debak, Kabong, Lingga, Engkelili,
            Betong, Spaoh, Pusa, Saratok
          </option>
          <option value="SWK07" class="hs">SWK07 - Serian, Simunjan, Samarahan, Sebuyau, Meludam</option>
          <option value="SWK08" class="hs">SWK08 - Kuching, Bau, Lundu, Sematan</option>
          <option value="SWK09" class="hs">SWK09 - Zon Khas (Kampung Patarikan)</option>
        </optgroup>
        <optgroup label="Terengganu">
          <option value="TRG01" class="hs">TRG01 - Kuala Terengganu, Marang, Kuala Nerus</option>
          <option value="TRG02" class="hs">TRG02 - Besut, Setiu</option>
          <option value="TRG03" class="hs">TRG03 - Hulu Terengganu</option>
          <option value="TRG04" class="hs">TRG04 - Dungun, Kemaman</option>
        </optgroup>
        <optgroup label="Wilayah Persekutuan">
          <option value="WLY01" class="hs">WLY01 - Kuala Lumpur, Putrajaya</option>
          <option value="WLY02" class="hs">WLY02 - Labuan</option>
        </optgroup>
      </select>
<!-- Button to Get Prayer Time     -->
      <button @click="LoadPrayerTimes(period,zone)" class="ml-auto px-4 py-2 bg-amber-500 shadow text-white my-2 border border-transparent transition rounded-md hover:shadow-md active:shadow active:border-amber-900">
        <span v-if="!isLoading">Load Prayer Times</span>
        <div v-else class="flex items-center">
          <svg
              class="animate-spin h-5 w-5 mr-2 text-white"
              xmlns="http://www.w3.org/2000/svg"
              fill="none"
              viewBox="0 0 24 24"
          >
            <circle
                class="opacity-25"
                cx="12"
                cy="12"
                r="10"
                stroke="currentColor"
                stroke-width="4"
            ></circle>
            <path
                class="opacity-75"
                fill="currentColor"
                d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
            ></path>
          </svg>
          <span>Loading...</span>
        </div>
      </button>
    </div>
<!--  Prayer Times Table  -->
    <div class="overflow-x-auto rounded-lg shadow">
      <table class="min-w-full bg-white">
        <thead class="bg-gray-50 border-b">
        <tr>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Hijri</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Date</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Day</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Imsak</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Subuh</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Syuruk</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Zohor</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Asar</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Maghrib</td>
          <td class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Isyak</td>
        </tr>
        </thead>
        <tbody class="divide-y divide-gray-200">
        <tr v-for="(row, index) in prayerTimes"
            :key="index"
            :class="index % 2 === 0 ? 'bg-white' : 'bg-gray-50'">
          <td v-for="(value, key) in row"
              :key="key"
              class="px-6 py-4 whitespace-nowrap text-sm text-gray-900">
            {{ value }}
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>

</template>

<style >
body{
  @apply bg-amber-100
}
</style>
