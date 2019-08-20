<template>
  <div :style="window.style">
    <div :style="windowSize">
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
        width: 1920,
        height: 1080,
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
      return `width: ${this.window.width}px;height: ${this.window.height}px;`
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
      this.window.style = `zoom: ${Math.min(scale, 1)};`
    }
  }
}
</script>

<style>
</style>
