<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" @click="open">
    <Team ref="teamRef" />
  </div>
</template>

<script>
import Team from './ModalTeam.vue'

export default {
  name: 'App',
  components: {
    Team
  },
  methods: {
    open() {
      this.$refs.teamRef.init()
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
</style>
