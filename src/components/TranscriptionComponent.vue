<template>
  <main>
    <p>{{ transcription }}</p>
  </main>
</template>

<script>
export default {
  name: 'TranscriptionComponent',
  props: [
    'transcription'
  ],
  data () {
    return {
    }
  }
}
</script>

<style scoped>
  main {
    display: flex;
    justify-content: center;
		animation-duration: 333s;
		animation-fill-mode: both;
  }

  p {
    font-size: 1.3em;
    max-width: 30em;
    margin: .5em 2em;
    padding: 1em;
    background-color: #FFFFFF;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
		opacity: .666;
  }
</style>
