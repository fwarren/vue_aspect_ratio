<template>
  <div :style="window.style">
    <div style="width: 1680px;height: 1050px;background-image: url('https://wallpapercave.com/wp/mvdjImO.jpg')">
      <router-view/>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: function () {
    return {
      window: {
        width: 1680,
        height: 1050,
        style: ''
      }
    }
  },
  created () {
    window.addEventListener('resize', this.handleResize)
    this.handleResize()
  },
  destroyed () {
    window.removeEventListener('resize', this.handleResize)
  },
  computed: {
    windowSize: function () {
      return `width: ${this.window.width};height: ${this.window.height}`
    }
  },
  methods: {
    handleResize () {
      var appWidth = window.innerWidth
      var appHeight = window.innerHeight
      var ratio = appHeight / appWidth
      var originalRatio = this.window.height / this.window.width
      var scale = 1
      if (ratio === originalRatio) {
      } else if (ratio > originalRatio) {
        // extra height so zoom  for width ratio
        scale = appWidth / this.window.width
      } else {
        // extra width so zoom for height ratio
        scale = appHeight / this.window.height
      }
      this.window.style = `zoom: ${scale};`
    }
  }
}
</script>

<style>
</style>
