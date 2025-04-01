<template>
    <div class="timer">
      <h2>{{ formatTime }}</h2>
      <p> {{ cycleMessage }}</p>
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
        cycle: "work",
        workTime: 25 * 60,
        breakTime: 5 * 60,
      };
    },
    computed: {
      formatTime() {
        const minutes = Math.floor(this.time / 60);
        const seconds = this.time % 60;
        return `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(2, "0")}`;
      },
      cycleMessage() {
      return this.cycle === "work" ? "Hora do foco!" : "Hora do descanso!";
    }
    },
    methods: {
      startTimer() {
        if (!this.isRunning) {
          this.isRunning = true;
          this.interval = setInterval(() => {
            if (this.time > 0) {
              this.time--;
            } else {
              this.switchCycle()
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
        this.cycle = "work"
        this.time = 25 * 60;
      },
      switchCycle() {
        clearInterval(this.interval);
        this.isRunning = false;

        if (this.cycle === "work") {
          this.cycle = "break";
          this.time = this.breakTime;
        } else {
          this.cycle = "work";
          this.time = this.workTime;
        }

        this.startTimer()
      }
    },
  };
  </script>
  
  <style scoped>
  .timer {
    text-align: center;
    margin-top: 20px;
    background: linear-gradient(135deg, #ff4b2b, #ff416c);
    padding: 30px;
    border-radius: 15px;
    color: white;
    width: 300px;
    margin: auto;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  }

  h2 {
    font-size: 48px;
    font-weight: bold;
    margin: 10px 0
  }

  p {
    font-size: 18px;
    font-weight: 500;
    margin-bottom: 20px;
  }
  
  button {
    background-color: white;
    color: #ff416c;
    border: none;
    padding: 12px 20px;
    margin: 5px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    border-radius: 15px;
    transition: 0.3s;
  }

  button:hover {
    background-color: rgba(255, 255, 255, 0.8)
  }
  
  button:disabled {
    background-color: rgba(255, 255, 255, 0.5);
    cursor: not-allowed;
  }
  </style>
  