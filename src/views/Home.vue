<template>
  <div class="home">
    <HelloWorld :msg='msg'></HelloWorld>
    <div class='box'>{{dpr}}</div>
    <div class='box2'></div>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data(){
    return {
      msg: 'hello,this is homepage!',
      dpr:0
    }
  },
  created(){
    //this.dpr = window.devicePixelRatio
  }
}
</script>

<style>
  .box2{
    width:750px;
    height:100px;
    background-color:green;
  }
</style>
