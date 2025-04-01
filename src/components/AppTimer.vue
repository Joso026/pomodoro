<template>
    <div class="timer">
      <h2>{{ formatTime }}</h2>
      <button @click="startTimer" :disabled="isRunning">Iniciar</button>
      <button @click="pauseTimer" :disabled="!isRunning">Pausar</button>
      <button @click="resetTimer">Resetar</button>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        time: 25 * 60, // 25 minutos em segundos
        isRunning: false,
        interval: null,
      };
    },
    computed: {
      formatTime() {
        const minutes = Math.floor(this.time / 60);
        const seconds = this.time % 60;
        return `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;
      },
    },
    methods: {
      startTimer() {
        if (!this.isRunning) {
          this.isRunning = true;
          this.interval = setInterval(() => {
            if (this.time > 0) {
              this.time--;
            } else {
              clearInterval(this.interval);
              this.isRunning = false;
            }
          }, 1000);
        }
      },
      pauseTimer() {
        this.isRunning = false;
        clearInterval(this.interval);
      },
      resetTimer() {
        this.isRunning = false;
        clearInterval(this.interval);
        this.time = 25 * 60;
      },
    },
  };
  </script>
  
  <style scoped>
  .timer {
    text-align: center;
    margin-top: 20px;
  }
  
  button {
    margin: 5px;
    padding: 10px;
    font-size: 16px;
    cursor: pointer;
  }
  
  button:disabled {
    background-color: #ccc;
    cursor: not-allowed;
  }
  </style>
  