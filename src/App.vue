<template>
  <div id="app">
    <h1>Pomodoro Timer</h1>
    <AppTimer />
  </div>
</template>

<script>
import AppTimer from './components/AppTimer.vue';

export default {
  components: {
    AppTimer,
  }
}
</script>

<style>
#app {
  text-align: center;
  font-family: Arial, Helvetica, sans-serif;
  padding: 20px;
}
</style>
