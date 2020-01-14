<template>
  <div id="app">
    <FortuneWheel :sections="sections" />
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
      sections: [
        {
          id: 1,
          title: '100',
          color: 'tomato'
        },
        {
          id: 2,
          title: '200',
          color: 'khaki'
        },
        {
          id: 3,
          title: '300',
          color: 'darkseagreen'
        }
      ]
    }
  }
}
</script>

<style>
  body {
    background: black;
  }
#app {
  font-family: sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
