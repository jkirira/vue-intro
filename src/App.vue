<template>
  <div id="app">
    <div class="carousel">
      
      <div class="image-left">
        <img v-if="if_toggle"  alt="Vue logo" src="./assets/logo.png">
      </div>
      
      <div class="image-center">
        <img alt="Vue logo" src="./assets/logo.png">
      </div>
      
      <div class="image-right">
        <img v-show="show_toggle"  alt="Vue logo" src="./assets/logo.png">
      </div>
      
    </div>
    <div class="toggles">
      <p>Check the boxes to toggle the images above</p>
      <div class="toggle-wrapper">
        <div>
          <input type="checkbox" @change="if_toggle = !if_toggle"> Remove Left Image
       </div>
        
        <div>
          <input type="checkbox" @change="toggle_show">Remove Right Image
        </div>
        
      </div>
    </div>
    
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data(){
    return {
      if_toggle: true,
      show_toggle: true,
    }
  },
  methods: {
    toggle_show: function(){
      this.show_toggle = !this.show_toggle
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.toggle-wrapper{
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
}
.carousel{
  display: flex;
  align-items: center;
  justify-content: center;
}
.image-center{
  border: 3px solid greenyellow;
  box-sizing: border-box;
  padding: 5px;
  margin: 5px;
  border-radius: 10px;
  display: flex;
}
</style>
