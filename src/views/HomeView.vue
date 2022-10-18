<template>
  <div class="flex flex-col h-screen max-h-screen">
    <!-- Search / Results -->
    <div
      class="flex justify-center relative bg-hero bg-cover px-4 pt-8 pb-32 z-20"
    >
      <!-- Search Input -->
      <div class="w-full max-w-screen-sm">
        <h1 class="text-white text-center text-3xl pb-4">IP Address Tracker</h1>
        <div class="flex">
          <input
            class="flex-1 py-3 px-2 rounded-tl-md rounded-bl-md"
            type="text"
            placeholder="Search for an IP address or leave empty for yours"
            v-model="userInput"
          />
          <i
            @click="getIpDetails"
            class="fas fa-chevron-right cursor-pointer bg-black text-white px-4 rounded-tr-md rounded-br-md flex items-center"
          ></i>
        </div>
      </div>
      <!-- IPINFO COMPONENT -->
      <IPInfo v-if="ipDetails" :ipDetails="ipDetails" />
    </div>
    <div id="map" class="h-full z-10"></div>
  </div>
</template>

<script>
import { onMounted, ref } from 'vue';
import IPInfo from '@/components/IPInfo';
import leaflet from 'leaflet';
import axios from 'axios';

export default {
  components: { IPInfo },

  setup() {
    const userInput = ref('');
    const ipDetails = ref(null);

    // get map
    let loadmap;
    onMounted(() => {
      loadmap = leaflet.map('map').setView([51.505, -0.09], 13);
      leaflet
        .tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
          maxZoom: 19,
          attribution:
            '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>',
        })
        .addTo(loadmap);
    });

    // get user ip/ search ip
    const getIpDetails = async () => {
      const url = `https://geo.ipify.org/api/v2/country,city?apiKey=at_LBmIjaXG1jkVJyeWczaQRWasDx9S1&ipAddress=${userInput.value}`;

      try {
        const data = await axios.get(url);
        const res = data.data;
        userInput.value = '';
        ipDetails.value = {
          address: res.ip,
          state: res.location.region,
          timezone: res.location.timezone,
          isp: res.isp,
          lat: res.location.lat,
          lng: res.location.lng,
        };
        leaflet
          .marker([ipDetails.value.lat, ipDetails.value.lng])
          .addTo(loadmap);

        loadmap.setView([ipDetails.value.lat, ipDetails.value.lng], 13);
      } catch (err) {
        alert(err.message);
      }
    };

    return { userInput, ipDetails, getIpDetails };
  },
};
</script>

