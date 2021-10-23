<template>
  <div class="home">
    <div id="mapContainer"></div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from "@/components/HelloWorld.vue";
import "leaflet/dist/leaflet.css";
import axios from 'axios';
import L from "leaflet";
export default {
  name: "Home",
  components: {
    HelloWorld,
  },
  data() {
    return {
      currentWeather: null,
      center: [37, 7749, -122, 4194],
    };
  },
  methods: {
    setupLeafletMap: function () {
      const mapDiv = L.map("mapContainer").setView([52.6042, 39.5938], 13);
      L.tileLayer(
        "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
        {
          attribution:
            'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
          maxZoom: 18,
          id: "dsh16/ckv3ennau4mvn14qkxgtw8clm",
          tileSize: 512,
          zoomOffset: -1,
          accessToken:
            "pk.eyJ1IjoiZHNoMTYiLCJhIjoiY2t2M2Q5OHU2MGxoaDJ1czMxaGs0dW03NSJ9.5nyAAHMveJrg5uL46uFVvQ",
        }
      ).addTo(mapDiv);
    },
  },
  mounted() {
    axios
      .get("http://api.openweathermap.org/data/2.5/weather?q=Lipetsk&lang=ru&units=metric&appid=fd965aaa128624a747e3ff8c08b58442")
      .then((response) => (this.currentWeather = response));

    this.setupLeafletMap();
  },
};
</script>

<style scoped>
#mapContainer {
  margin: auto;
  width: 80vw;
  height: 100vh;
}
</style>