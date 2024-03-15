<template>
  <div class="circle-progress-bar">
    <svg class="circle" :width="size" :height="size">
      <circle 
        class="track" 
        :r="radius" 
        :cx="center" 
        :cy="center" 
        :stroke-width="strokeWidth" 
      />
      <circle 
        class="progress" 
        :r="radius" :cx="center" 
        :cy="center" 
        stroke-linecap="round" 
        :stroke-width="strokeWidth" 
        :stroke-dasharray="circumference" 
        :stroke-dashoffset="offset" 
      />
      <text 
        class="percentage" 
        :x="center" 
        :y="center" 
        text-anchor="middle" 
        dominant-baseline="middle" 
        transform="rotate(90,100,100)"
      >
        {{ progress || 0 }}%
      </text>
    </svg>
    <input class="progress-controller" type="text" v-model="progress" @input="updateProgress" placeholder="Enter value from 0 to 100" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      progress: '',
      size: 200,
      strokeWidth: 20,
    };
  },
  computed: {
    radius() {
      return (this.size - this.strokeWidth) / 2;
    },
    center() {
      return this.size / 2;
    },
    circumference() {
      return 2 * Math.PI * this.radius;
    },
    offset() {
      return this.circumference * (1 - this.progress / 100);
    },
  },
  methods: {
    autoFillProgress() {
      const interval = setInterval(() => {
        this.progress += 1;
        if (this.progress > 100) {
          this.progress = 0;
        }
      }, 100);
      setTimeout(() => {
        clearInterval(interval);
        this.progress = ''
      }, 10000);
    },
    updateProgress() {
      this.progress = this.progress.replace(/\D/g, '');
      if (this.progress < 0) this.progress = 0;
      if (this.progress > 100) this.progress = 100;
    }
  },
  mounted() {
    this.autoFillProgress()
  }
};
</script>

<style scoped>
.track .progress {
  margin: 15px;
}

.circle-progress-bar {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #231540;
}

.circle {
  transform: rotate(-90deg);
}

.track {
  fill: none;
  stroke: #4F4466;
}

.progress {
  fill: none;
  stroke: #EBE424;
  transition: stroke-dashoffset 0.3s ease-in-out;
  filter: drop-shadow(0 0 3px #fdf629);
}

.percentage {
  font-family: Arial, sans-serif;
  font-size: 38px;
  fill: #EBE424;
}

.progress-controller {
  margin-top: 10px;
  width: 200px;
  text-align: center;
  border: none;
  background-color: #4F4466;
  padding: 8px;
  font-size: 16px;
  color: #EBE424;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.progress-controller:focus {
  outline: none;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
}

.circle circle {
  margin: 10px; /* Добавлено свойство margin для задания отступа */
}
</style>
