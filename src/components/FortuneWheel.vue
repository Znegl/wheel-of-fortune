<template>
  <svg viewBox="0 0 42 42">
    <WheelSection
      v-for="(section, index) in sections"
      :key="section.id"
      :data="section"
      :start-angle="getStartAngle(index)"
      :end-angle="getEndAngle(index)"
      :wheel-center="21"
      :wheel-radius="21"
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