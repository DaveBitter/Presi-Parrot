<template>
  <main>
    <h1>{{ text }}</h1>
  </main>
</template>

<script>
export default {
  name: 'HelperText',
  props: [
    'text'
  ],
  data () {
    return {
    }
  }
}
</script>

<style scoped>
  main {
    position: fixed;
    top: 40vh;
    right: 0;
    bottom: 0;
    left: 0;
  }

  h1 {
    font-size: 2.5em;
    text-align: center;
    opacity: .3;
  }
</style>
