<template>
  <div id="app">
    <h1>Stopwatch</h1>
    <div class="timer">{{ formatTime }}</div>
    <div class="controls">
      <button @click="start">Start</button>
      <button @click="stop">Stop</button>
      <button @click="reset">Reset</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      startTime: null,
      elapsedTime: 0,
      timer: null,
    };
  },
  computed: {
    formatTime() {
      const milliseconds = this.elapsedTime % 1000;
      const seconds = Math.floor((this.elapsedTime / 1000) % 60);
      const minutes = Math.floor((this.elapsedTime / 1000 / 60) % 60);
      const hours = Math.floor(this.elapsedTime / 1000 / 60 / 60);

      return `${hours.toString().padStart(2, "0")}:${minutes.toString().padStart(2, "0")}:${seconds.toString().padStart(2, "0")}.${milliseconds.toString().padStart(3, "0")}`;
    },
  },
  methods: {
    start() {
      if (!this.timer) {
        this.startTime = Date.now() - this.elapsedTime;
        this.timer = setInterval(() => {
          this.elapsedTime = Date.now() - this.startTime;
        }, 10);
      }
    },
    stop() {
      clearInterval(this.timer);
      this.timer = null;
    },
    reset() {
      this.elapsedTime = 0;
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

.timer {
  font-size: 48px;
  margin-bottom: 20px;
}

.controls button {
  margin: 5px;
}
</style>
