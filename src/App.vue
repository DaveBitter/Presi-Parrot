<template>
  <main id="app">
    <IdleComponent v-show='mode === "idle"' />
    <TranscriptionContainer v-show='mode === "active"' />
  </main>
</template>

<script>
import TranscriptionContainer from './components/TranscriptionContainer'
import IdleComponent from './components/IdleComponent'

export default {
  name: 'app',
  components: {
    TranscriptionContainer,
    IdleComponent
  },
  data() {
    return{
      mode: 'idle'
    }
  },
	created() {
		this.$on('startParrot', () => this.mode = 'active')
		this.$on('stopParrot', () => this.mode = 'idle')
	}
}
</script>

<style>
  body {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    margin: 0;
    background-color: #FFD026;
  }

  main#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    display: flex;
    justify-content: center;
  }
</style>
