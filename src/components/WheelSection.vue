<template>
  <g>
    <path :fill="data.color" :d="path"/>
    <text :x="wheelCenter + centerOffset + (wheelRadius - centerOffset) / 2" :y="wheelCenter" :transform="`rotate(${-textAngle} ${wheelCenter} ${wheelCenter})`" text-anchor="middle">
      {{data.title}}
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
      centerOffset: {
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
        const innerStartCoordinate = this.angleToCoordinate(this.startAngle, this.centerOffset)
        const innerEndCoordinate = this.angleToCoordinate(this.endAngle, this.centerOffset)

        const outerStartCoordinate = this.angleToCoordinate(this.startAngle, this.wheelRadius)
        const outerEndCoordinate = this.angleToCoordinate(this.endAngle, this.wheelRadius)

        return [
          `M${innerStartCoordinate.x} ${innerStartCoordinate.y}`,
          `L${outerStartCoordinate.x} ${outerStartCoordinate.y}`,
          `A${this.wheelRadius} ${this.wheelRadius} 0 0 0 ${outerEndCoordinate.x} ${outerEndCoordinate.y}`,
          `L${outerEndCoordinate.x} ${outerEndCoordinate.y}`,
          `L${innerEndCoordinate.x} ${innerEndCoordinate.y}`,
          `A${this.centerOffset} ${this.centerOffset} 0 0 1 ${innerStartCoordinate.x} ${innerStartCoordinate.y}`,
        ].join(' ')
      },
      textAngle() {
        return (this.startAngle + this.endAngle) / 2
      }
    },
    methods: {
      angleToCoordinate(angle, radius) {
        const radians = this.degreesToRadians(angle, radius)
        const x = Math.cos(radians) * radius + this.wheelCenter
        const y = this.wheelCenter - Math.sin(radians) * radius

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
    font-family: Bubblegum Sans, sans-serif;
    font-weight: bold;
    font-size: 4px;
  }
</style>