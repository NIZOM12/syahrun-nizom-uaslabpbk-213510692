<template>
  <div id="app">
    <h1>Widget Foto</h1>
    <div class="image-container">
      <img v-if="imageUrl" :src="imageUrl" alt="Foto Terpilih" @click="toggleImageSize" :class="{ enlarged: isEnlarged }" />
    </div>
    <button @click="getRandomPhotos" :disabled="loading">Pilih Foto Random</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      imageUrl: "",
      loading: false,
      isEnlarged: false,
    };
  },
  methods: {
    onFileChange(event) {
      const file = event.target.files[0];
      if (file && file.type.includes("image")) {
        this.imageUrl = URL.createObjectURL(file);
      }
    },
    getRandomPhotos() {
      (this.loading = true),
        fetch("https://source.unsplash.com/random")
          .then((response) => {
            this.imageUrl = response.url;
            this.loading = false;
          })
          .catch((error) => {
            console.error(error);
            this.loading = false;
          });
    },
    toggleImageSize() {
      this.isEnlarged = !this.isEnlarged;
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  margin-top: 20px;
}

h1 {
  font-size: 24px;
  margin-bottom: 20px;
}

.image-container {
  margin-top: 20px;
}

.image-container img {
  max-width: 300px;
  max-height: 300px;
}
</style>
