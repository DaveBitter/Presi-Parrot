<template>
  <section id='transcription-container'>
		<article v-show='liveTranscription || transcriptions.length' id='live-transcription'>
			<p>{{ liveTranscription }}</p>
		</article>
    <article id='historical-transcriptions' v-if='transcriptions.length'>
      <section  v-for='transcription in transcriptions'>
        <TranscriptionComponent :transcription='transcription' />
      </section>
    </article>
    <article v-else='transcriptions.length'>
      <section>
        <HelperText v-show='!liveTranscription' :text='"Start talking to see your transcriptions"' />
      </section>
    </article>
		<img id='stop' src='../assets/stop.svg' v-on:click='stopParrot' />
  </section>
</template>

<script>
  import TranscriptionComponent from './TranscriptionComponent'
  import HelperText from './HelperText'

  export default {
    name: 'TranscriptionContainer',
    components: {
      TranscriptionComponent,
      HelperText
    },
    data () {
      return {
				liveTranscription: null,
        transcriptions: [
        ],
        mode: null,
        commands: [
          'start',
          'stop',
        ]
      }
    },
    methods: {
      startParrot() {
        this.mode = 'active'
        window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
        const recognition = new SpeechRecognition();
        recognition.interimResults = true;
        recognition.lang = 'en-US';

        recognition.addEventListener('result', event => {
          this.handleTranscription(event)
        })

        recognition.addEventListener('end', () => {
          if(this.mode === 'active') recognition.start()
        })
        recognition.start();
      },
      handleTranscription(event, cb) {
        const transcription = Array.from(event.results)
          .map(result => result[0])
          .map(result => result.transcript)
          .join('');

				console.log(transcription)

        if (event.results[0].isFinal) {
					this.liveTranscription = ''
        	this.transcriptions.unshift(transcription)
        } else {
					this.liveTranscription = transcription
				}
      },
			stopParrot() {
				this.transcriptions = []
				this.$parent.$emit('stopParrot')
			}
    },
    created() {
      this.startParrot()
    }
}
</script>

<style scoped>
	article#live-transcription {
		font-size: 1.6em;
    width: 50vw;
    margin: .5em 2em;
    padding: 1em;
    background-color: #FFFFFF;
    box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
	}

  article#historical-transcriptions {
    max-height: 75vh;
    overflow-y: auto;
  }

  article#historical-transcriptions::-webkit-scrollbar {
    display: none;
  }

  h1 {
    margin: 0;
  }

	img#stop {
		position: absolute;
		right: 45vw;
		bottom: 5vh;
		left: 45vw;
		width: 10vw;
		height: 10vw;
		cursor: pointer;
		transition: 66ms ease-out;
	}

	img#stop:hover {
		right: 38vw;
		bottom: 3vh;
		left: 43vw;
		width: 14vw;
		height: 14vw;
	}
</style>
