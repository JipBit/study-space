<template>
    <div class="bg-[#1B1C1F] text-white mt-12 p-4 rounded-t-md">
        <div class="sm:text-7xl text-6xl font-bold flex flex-col justify-center h-screen items-center text-center bg-[#3C3E44] rounded-md" id="timer">
            <div>
              <span id="minutes">{{ minutes }}</span>
              <span id="middle">:</span>
              <span id="seconds">{{ seconds }}</span>
            </div>
            
            <div class="flex items-center justify-center space-x-3">
                <svg class="bg-[#2B2D31] rounded-full p-2 mt-10 cursor-pointer" @click="stopTimer()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" style="fill: rgba(255, 255, 255, 1);transform: ;msFilter:;"><path d="M7 7h10v10H7z"></path></svg>
                <button :disabled="clicked" @click="startTimer()">
                  <svg class="bg-[#2B2D31] rounded-full p-2 mt-10 cursor-pointer" xmlns="http://www.w3.org/2000/svg" width="64" height="64" viewBox="0 0 24 24" style="fill: rgba(255, 255, 255, 1);transform: ;msFilter:;"><path d="M7 6v12l10-6z"></path></svg>
                </button>
                <svg class="bg-[#2B2D31] rounded-full p-2 mt-10 cursor-pointer" @click="resetTimer()" xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" style="fill: rgba(255, 255, 255, 1);transform: ;msFilter:;"><path d="M10 11H7.101l.001-.009a4.956 4.956 0 0 1 .752-1.787 5.054 5.054 0 0 1 2.2-1.811c.302-.128.617-.226.938-.291a5.078 5.078 0 0 1 2.018 0 4.978 4.978 0 0 1 2.525 1.361l1.416-1.412a7.036 7.036 0 0 0-2.224-1.501 6.921 6.921 0 0 0-1.315-.408 7.079 7.079 0 0 0-2.819 0 6.94 6.94 0 0 0-1.316.409 7.04 7.04 0 0 0-3.08 2.534 6.978 6.978 0 0 0-1.054 2.505c-.028.135-.043.273-.063.41H2l4 4 4-4zm4 2h2.899l-.001.008a4.976 4.976 0 0 1-2.103 3.138 4.943 4.943 0 0 1-1.787.752 5.073 5.073 0 0 1-2.017 0 4.956 4.956 0 0 1-1.787-.752 5.072 5.072 0 0 1-.74-.61L7.05 16.95a7.032 7.032 0 0 0 2.225 1.5c.424.18.867.317 1.315.408a7.07 7.07 0 0 0 2.818 0 7.031 7.031 0 0 0 4.395-2.945 6.974 6.974 0 0 0 1.053-2.503c.027-.135.043-.273.063-.41H22l-4-4-4 4z"></path></svg>
            </div>
        </div>
    </div>
</template>

<script>
const alarmSound = require("@/assets/ring_a_ding.mp3").default;

export default {
  data() {
    return {
      timer: null,
      totalTime: 25 * 60,
      resetButton: false,
      clicked: false,
      alarmSound,
    };
  },

  methods: {
    startTimer() {
      this.clicked = true;

      this.timer = setInterval(() => this.countdown(), 1000);
    },

    stopTimer() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
      this.clicked = false;
    },

    resetTimer() {
      this.totalTime = 25 * 60;
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
      this.clicked = false;
    },

    padTime(time) {
      return (time < 10 ? "0" : "") + time;
    },

    countdown() {
      if (this.totalTime >= 1) {
        this.totalTime--;
      } else {
        this.totalTime = 0;
        var audio = new Audio(this.alarmSound);
        audio.play();
        this.resetTimer();
        this.clicked = false;
      }
    },
  },

  computed: {
    minutes() {
      const minutes = Math.floor(this.totalTime / 60);

      return this.padTime(minutes);
    },

    seconds() {
      const seconds = this.totalTime - this.minutes * 60;

      return this.padTime(seconds);
    },
  },
};
</script>

<style>

</style>