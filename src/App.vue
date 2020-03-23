<template>
  <div id="app">
    <Quiz />
  </div>
</template>

<script>
import Quiz from './components/Quiz';

export default {
  name: 'App',
  components: {
    Quiz
  }
}
</script>

<style lang="scss">
html,body{
  width: 100%;
  height: 100%;
  padding: 0;
  margin: 0;
}
</style>
