<template>
  <div id="app">
    <div class="carousel">
      <div class="control">
        <button class="btn" @click="previous()">Previous</button>
        <button class="btn" @click="next()">Next</button>
      </div>
      <!-- <transition name="component-fade" mode="out-in">
        <component v-bind:is="view[currentCount % view.length]" v-on: mouseover="stopRotation" v-on: mouseout="startRotation"></component>
      </transition> -->
      <div class="slides" v-on: mouseover="stopRotation" v-on: mouseout="startRotation">
        <transition name="component-fade" mode="out-in">
            <component v-bind:is="view[currentCount % view.length]"></component>
        </transition>
        <transition name="component-fade" mode="out-in">
            <component v-bind:is="view[(currentCount + 1) % view.length]"></component>
        </transition>
        <transition name="component-fade" mode="out-in">
            <component v-bind:is="view[(currentCount + 2) % view.length]"></component>
        </transition>
       </div>
      </div>
      <div class="dots">
          <div class="single-dot" v-for="(item,index) in view" v-on:click="activeComponent(index)" :style="`background-color: ${(index === currentCount%view.length) ? dotActiveColor : dotInactiveColor};`"></div>
      </div>
      <div class="thumbnails">
        <ul>
          <li v-for="(item,index) in view" v-on:click="activeComponent(index)" :style="`opacity: ${(index === currentCount%view.length) ? 0.4 : 1};`">
            <component v-bind:is="item"></component>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      view: ['comp-a', 'comp-b', 'comp-c'],
      timer: null,
      currentCount: 0,
      autoplayTimeout: 3000,
      imageActiveOpacity: '0.4',
      dotActiveColor: '#000',
      dotInactiveColor: '#b3b3b3'
    }
  },
  components: {
    'comp-a': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557407_1000.jpg" alt="image1" width="256">'
    },
    'comp-b': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557409_1000.jpg" alt="image2" width="256">'
    },
    'comp-c': {
      template: '<img src="https://cdn-images.farfetch-contents.com/12/13/10/56/12131056_10557410_1000.jpg" alt="image3" width="256">'
    }
  },
  mounted: function () {
    this.startRotation()
  },
  methods: {
    startRotation: function () {
      this.timer = setInterval(this.next, this.autoplayTimeout)
    },
    stopRotation: function () {
      clearInterval(this.timer)
      this.timer = null
    },
    next: function () {
      this.currentCount += 1
    },
    previous: function () {
      this.currentCount -= 1
    },
    activeComponent: function (index) {
      this.currentCount = index
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

 .dots{
   
 }

 .single-dot{
   display: inline-block;
   margin-left: 4px; 
   width: 10px;
   height: 10px;
   border-radius: 50%;
   background-color: #b0b0b0;
 }
 .active-dot{
   background-color: #000;
 }
 
 .thumbnails ul li{
   display: inline;
   margin-left: 4px;
 }
 .thumbnails img{
   width:40px;
 }
 .thumbnails img .active{
   opacity: 0.4;
 }

</style>
