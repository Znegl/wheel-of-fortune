<template>
  <svg viewBox="0 0 100 100" class="fortune-wheel">
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
      }
    },
    computed: {
      totalSections() {
        return this.sections.length
      }
    },
    methods: {
      getStartAngle(index) {
        return 360 / this.totalSections * index
      },
      getEndAngle(index) {
        return 360 / this.totalSections * (index + 1)
      }
    }
  }
</script>

<style scoped>
  .fortune-wheel {
    display: block;
    width: 50vmin;
  }
</style>