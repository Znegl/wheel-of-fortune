<template>
  <g>
    <path :fill="data.color" :d="path"/>
    <text :x="wheelCenter" :y="wheelCenter" :transform="`rotate(${textAngle} ${wheelCenter} ${wheelCenter})`">
      {{data.title}} ({{startAngle}} - {{endAngle}})
    </text>
  </g>
</template>

<script>
  export default {
    name: 'WheelSection',
    props: {
      data: {
        type: Object,
        required: true
      },
      startAngle: {
        type: Number,
        required: true
      },
      endAngle: {
        type: Number,
        required: true
      },
      wheelCenter: {
        type: Number,
        required: true
      },
      wheelRadius: {
        type: Number,
        required: true
      }
    },
    computed: {
      path() {
        const startCoordinate = this.angleToCoordinate(this.startAngle)
        const endCoordinate = this.angleToCoordinate(this.endAngle)
        return [
          `M${this.wheelCenter} ${this.wheelCenter}`,
          `L${startCoordinate.x} ${startCoordinate.y}`,
          `L${endCoordinate.x} ${endCoordinate.y}`,
          `L${this.wheelCenter} ${this.wheelCenter}`,
        ].join(' ')
      },
      textAngle() {
        return (this.startAngle + this.endAngle) / 2
      }
    },
    methods: {
      angleToCoordinate(angle) {
        const radians = this.degreesToRadians(angle)
        const x = Math.cos(radians) * this.wheelRadius + this.wheelCenter
        const y = this.wheelCenter - Math.sin(radians) * this.wheelRadius

        return {x ,y}
      },
      degreesToRadians(degrees) {
        return degrees * Math.PI / 180
      }
    }
  }
</script>

<style scoped>
  text {
    font-size: 3px;
    fill: white;
  }
</style>