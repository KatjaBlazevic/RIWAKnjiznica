<template>
  <q-page padding>
    <!-- content -->
    <div id="map" style="height:500px;"></div>
  </q-page>
</template>

<script>
import { ref, onMounted } from "vue";
import * as L from "leaflet";
import "leaflet/dist/leaflet.css";

export default {
  setup() {
    const initialMap = ref(null);

    onMounted(() => {
      // Inicijalizacija mape
      initialMap.value = L.map("map").setView([45.3312, 14.4322], 13);

      // Dodavanje OpenStreetMap pločica
      L.tileLayer("https://tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 19,
        attribution:
          '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(initialMap.value);
    });

    return {
      initialMap,
    };
  },
};
</script>
