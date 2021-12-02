<template>
  <div class="home">
    <Map></Map>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import Map from '../components/Map.vue';

@Options({
  components: {
    HelloWorld,
    Map,
  },
})
export default class Home extends Vue {}
</script>
