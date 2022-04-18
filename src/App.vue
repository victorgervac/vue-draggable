<template>
  <h1>Rate The Movie</h1>
  <VueDraggableExample/>
  <TwoDraggableExample/>
</template>

<script>
import VueDraggableExample from './components/VueDraggableExample.vue';
import TwoDraggableExample from './components/TwoDraggableExample.vue';

export default {
  name: 'App',
  components: {
    VueDraggableExample,
    TwoDraggableExample,

  },
};
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
</style>
