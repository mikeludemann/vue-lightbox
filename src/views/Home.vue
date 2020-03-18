<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <lightbox :images='[{source: require("../assets/doctor-mario-world.jpg"), alttext: "Doctor Mario World"},{source: require("../assets/mario-kart-tour.png"), alttext: "Mario Kart Tour"}]'/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue';
import lightbox from '@/components/lightbox.vue';

export default {
  name: 'Home',
  components: {
    HelloWorld,
    lightbox
  }
}
</script>
