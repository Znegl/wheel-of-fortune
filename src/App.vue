<template>
  <div id="app">
    <div class="wheel-wrapper">
      <div class="arrow"></div>
      <FortuneWheel :sections="sections" :rotate="rotate" />
    </div>
  </div>
</template>

<script>
  import FortuneWheel from "./components/FortuneWheel";

  export default {
    name: 'app',
    components: {
      FortuneWheel
    },
    data() {
      return {
        rotate: true,
        sections: [
          {
            id: 1,
            title: 'Alle vinder 🥳',
            color: 'bisque'
          },
          {
            id: 2,
            title: 'Blå',
            color: 'cadetblue'
          },
          {
            id: 3,
            title: 'Fri bar',
            color: 'orange'
          },
          {
            id: 4,
            title: 'Pink',
            color: 'crimson'
          },
          {
            id: 5,
            title: 'Omtur',
            color: 'darkgray'
          },
          {
            id: 6,
            title: 'Grøn',
            color: 'darkolivegreen'
          },
          {
            id: 7,
            title: 'Orange',
            color: 'orangered'
          },
          {
            id: 8,
            title: 'Alle taber 😢',
            color: 'darkslategray'
          },
          {
            id: 9,
            title: 'Rød',
            color: 'darkred'
          }
        ]
      }
    },
    mounted() {
      document.body.addEventListener('keydown', () => {
        this.rotate = !this.rotate
      })
    }
  }
</script>

<style>
  body {
    padding: 0;
    margin: 0;
    background: black;
    overflow: hidden;
  }

  #app {
    font-family: sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
  }
  .wheel-wrapper {
    position: relative;
  }
  .arrow {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translate(-50%, -25%) scaleX(.5);
    border-color: white transparent transparent transparent;
    border-width: 5vmin;
    border-style: solid;
    z-index: 1;
  }
</style>
