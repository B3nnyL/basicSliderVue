<template>
  <div id="app">
    <div>
      <transition name="component-fade" mode="out-in">
        <component v-bind:is="view[currentCount % view.length]" v-on: mouseover="stopRotation" v-on: mouseout="startRotation"></component>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      view: ['v-a', 'v-b', 'v-c'],
      timer: null,
      currentCount: 0
    }
  },
  components: {
    'v-a': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557407_1000.jpg" alt="image1">'
    },
    'v-b': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557409_1000.jpg" alt="image2">'
    },
    'v-c': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557410_1000.jpg" alt="image3">'
    }
  },
  mounted: function () {
    this.startRotation()
  },
  methods: {
    startRotation: function () {
      this.timer = setInterval(this.next, 3000)
    },
    stopRotation: function () {
      clearInterval(this.timer)
      this.timer = null
    },
    next: function () {
      this.currentCount += 1
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  }

  .component-fade-enter-active, .component-fade-leave-active {
    transition: opacity .8s ease;
  }
  .component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active below version 2.1.8 */ {
    opacity: 0;
  }

 

</style>
