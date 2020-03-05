<template>
  <div class="home">
    <HelloWorld :msg='msg'></HelloWorld>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
console.log('........')
console.log('....3.....')
export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data(){
    return {
      msg: 'hello,this is homepage!'
    }
  }
}
</script>
