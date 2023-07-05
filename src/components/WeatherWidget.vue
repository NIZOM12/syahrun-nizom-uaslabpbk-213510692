<template>
  <div>
    <h2>Weather Widget</h2>
    <div class="search">
      <input type="text" v-model="location" placeholder="Masukkan nama kota atau negara" />
      <button @click="searchWeather">Cari</button>
    </div>
    <div v-if="errorMessage">{{ errorMessage }}</div>
    <div v-else-if="weather">
      <h3>{{ weather.name }}</h3>
      <p>Temperature: {{ weather.main.temp }}°C</p>
      <p>Weather: {{ weather.weather[0].description }}</p>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      location: "",
      weather: null,
      errorMessage: "",
    };
  },
  methods: {
    searchWeather() {
      if (this.location.trim() === "") {
        this.errorMessage = "Harap Masukkan nama kota";
        return;
      }
      axios
        .get(`https://api.openweathermap.org/data/2.5/weather?q=${this.location}&appid=b7bfca7b27a3485144fea086c50d09dc&units=metric`)
        .then((response) => {
          if (response.data.cod === "404") {
            this.errorMessage = "Kota tidak ditemukan";
            this.weather = null;
          } else {
            this.weather = response.data;
            this.errorMessage = "";
          }
        })
        .catch((error) => {
          console.error(error);
          this.errorMessage = "Terjadi kesalahan saat mengambil data cuaca";
          this.weather = null;
        });
    },
  },
};
</script>

<style>
.weather-widget {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  text-align: center;
}

h2 {
  font-size: 24px;
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
