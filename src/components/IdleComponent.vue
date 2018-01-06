<template>
  <section id='idle-component'>
    <article>
      <header>
        <HelperText :text='"Press start to start Presi Parrot"' />
      </header>
      <main>
      </main>
    </article>
  </section>
</template>

<script>
  import HelperText from './HelperText'
  export default {
    name: 'IdleComponent',
    components: {
      HelperText
    },
    data () {
      return {
     }
    }
}
</script>

<style scoped>
  section {
    display: flex;
    justify-content: center;
  }

  main {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  h1 {
    font-size: 2em;
  }

  h2 {
    font-size: 1.6em;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }
</style>
