<template>
  <section id='idle-component'>
    <article>
      <header>
        <HelperText :text='"Press the microphone to start Presi Parrot"' />
      </header>
      <main>
				<img id='start' src='../assets/microphone.svg' v-on:click='startParrot' />
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
    },
		methods: {
			startParrot() {
				this.$parent.$emit('startParrot')
			}
		}
}
</script>

<style scoped>
  section {
    display: flex;
    justify-content: center;
  }

	img#start {
		position: absolute;
		right: 40vw;
		bottom: 10vh;
		left: 40vw;
		width: 20vw;
		height: 20vw;
		cursor: pointer;
		transition: 66ms ease-out;
	}

	img#start:hover {
		right: 38vw;
		bottom: 8vh;
		left: 38vw;
		width: 24vw;
		height: 24vw;
	}
</style>
