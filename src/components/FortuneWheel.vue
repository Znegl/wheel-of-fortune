<template>
  <svg
    viewBox="0 0 100 100"
    class="fortune-wheel"
    :style="`--rotation: ${rotation}deg`"
  >
    <WheelSection
      v-for="(section, index) in sections"
      :key="section.id"
      :data="section"
      :start-angle="getStartAngle(index)"
      :end-angle="getEndAngle(index)"
      :center-offset="10"
      :wheel-center="50"
      :wheel-radius="50"
    />
    <circle cx="50" cy="50" r="5" :fill="centerFillColor"/>
  </svg>
</template>

<script>
  import WheelSection from "./WheelSection";

  export default {
    name: "FortuneWheel",
    components: {WheelSection},
    props: {
      sections: {
        type: Array,
        required: true
      },
      rotate: {
        type: Boolean,
        required: true
      }
    },
    data() {
      return {
        speed: 0,
        accelerationSpeed: 0.2,
        brakeSpeed: 0.015,
        minBrakeSpeed: 0.015,
        maxBrakeSpeed: 0.035,
        maxSpeed: 3,
        isStarting: false,
        isStopping: false,
        rotation: 0,
        rotationTimer: null,
        startStopTimer: null
      }
    },
    computed: {
      totalSections() {
        return this.sections.length
      },
      centerFillColor() {
        if(this.rotate) {
          return 'seagreen'
        } else {
          return 'tomato'
        }
      }
    },
    mounted() {
      setInterval(() => {
        if (this.rotate) {
          this.speed = Math.min(this.speed + this.accelerationSpeed, this.maxSpeed)
        } else {
          this.speed = Math.max(this.speed - this.brakeSpeed, 0)
        }
        this.rotation+= this.speed
      }, 50)
    },
    methods: {
      getStartAngle(index) {
        return 360 / this.totalSections * index
      },
      getEndAngle(index) {
        return 360 / this.totalSections * (index + 1)
      }
    },
    watch: {
      rotate() {
        const brakeSpeedDiff = this.maxBrakeSpeed - this.minBrakeSpeed
        this.brakeSpeed = Math.random() * brakeSpeedDiff + this.minBrakeSpeed
      }
    }
  }
</script>

<style scoped>
  .fortune-wheel {
    --rotation: 0deg;

    display: block;
    width: 99vmin;
    transform: rotate(var(--rotation));
    transition: transform 50ms linear;
  }
  circle {
    transition: fill .5s ease-out;
  }
</style>