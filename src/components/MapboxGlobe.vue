<template>
  <div ref="mapContainer" class="map-container"></div>
</template>

<script setup lang="ts">
import "mapbox-gl/dist/mapbox-gl.css";

import mapboxgl from "mapbox-gl"; // or "const mapboxgl = require('mapbox-gl');"
import { onMounted, ref } from "vue";

mapboxgl.accessToken =
  "pk.eyJ1IjoibGVvb3IyMiIsImEiOiJja3kzOWlrMjQwc3pmMnVwZW1jcGpzaWo2In0.7xaGhaIGCgsw3aQgmwqWFw";

const mapContainer = ref<HTMLElement>();

onMounted(() => {
  const map = new mapboxgl.Map({
    container: mapContainer.value!,
    style: "mapbox://styles/mapbox/streets-v11", // style URL
    // style: "mapbox://styles/mapbox/satellite-v9", // style URL
    center: [-74.5, 40], // starting position [lng, lat]
    zoom: 2, // starting zoom
    projection: "globe", // display the map as a 3D globe
  } as any);
  map.on("style.load", () => {
    map.setFog({
      color: "rgb(186, 210, 235)", // Lower atmosphere
      "high-color": "rgb(36, 92, 223)", // Upper atmosphere
      "horizon-blend": 0.02, // Atmosphere thickness (default 0.2 at low zooms)
      "space-color": "rgb(11, 11, 25)", // Background color
      "star-intensity": 0.6, // Background star brightness (default 0.35 at low zoooms )
    } as any); // Set the default atmosphere style
  });
});
</script>

<style scoped>
.map-container {
  width: 100vw;
  height: 100vh;
  /* background-color: red; */
}
</style>
