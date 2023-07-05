<template>
  <div class="location-widget"></div>

  <div>
    <h2>Location Widget</h2>
    <div class="search">
      <input type="number" v-model="latitude" placeholder="Latitude" />
      <input type="number" v-model="longitude" placeholder="Longitude" />
      <button @click="searchLocation">Cari</button>
    </div>
    <div v-if="errorMessage">{{ errorMessage }}</div>
    <div v-else-if="location">
      <h3>Your Location</h3>
      <p>Latitude: {{ location.latitude }}</p>
      <p>Longitude: {{ location.longitude }}</p>
      <p>
        City: <b>{{ location.components.city }}</b>
      </p>
      <p>
        Country: <b>{{ location.components.country }}</b>
      </p>
      <p>
        Postal Code: <b>{{ location.components.postcode }}</b>
      </p>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      latitude: null,
      longitude: null,
      location: null,
      errorMessage: "",
    };
  },
  mounted() {
    if (navigator.geolocation) {
      navigator.geolocation.getCurrentPosition(this.setInitialLocation, this.handleLocationError);
    }
  },
  methods: {
    setInitialLocation(position) {
      this.latitude = position.coords.latitude;
      this.longitude = position.coords.longitude;
      this.searchLocation();
    },
    handleLocationError(error) {
      console.error(error);
      this.errorMessage = "Terjadi kesalahan dalam mengambil lokasi awal";
    },
    searchLocation() {
      if (!this.latitude || !this.longitude) {
        this.errorMessage = "Harap masukkan latitude dan longitude";
        return;
      }
      axios
        .get(`https://api.opencagedata.com/geocode/v1/json?q=${this.latitude}+${this.longitude}&key=92591005a7b94008909d59a64b6d2a49`)
        .then((response) => {
          if (response.data.results.length === 0) {
            this.errorMessage = "Lokasi tidak ditemukan";
            this.location = null;
          } else {
            this.location = response.data.results[0];
            this.errorMessage = "";
          }
        })
        .catch((error) => {
          console.error(error);
          this.errorMessage = "Terjadi kesalahan saat mengambil data lokasi";
          this.location = null;
        });
    },
  },
};
</script>

<style>
h2 {
  font-size: 24px;
  margin-bottom: 20px;
}

.location-widget {
  margin-bottom: 20px;
}

.search {
  display: flex;
  justify-content: center;
  margin-bottom: 10px;
}

.search input {
  padding: 5px;
  margin-right: 5px;
}

.search button {
  padding: 5px 10px;
}

.error {
  color: red;
  margin-bottom: 10px;
}

.loading {
  margin-bottom: 10px;
}
</style>
