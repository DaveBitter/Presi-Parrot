<template>
  <section id='transcription-container'>
    <article v-if='transcriptions.length'>
      <section v-for='transcription in transcriptions'>
        <TranscriptionComponent :transcription='transcription' />
      </section>
    </article>
    <article v-else='transcriptions.length'>
      <section>
        <HelperText :text='"Start talking to see you transcriptions"' />
      </section>
    </article>
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
      endParrot() {
        recognition.stop()
        this.mode = 'idle'
        this.transcriptions = []
      },
      handleTranscription(event, cb) {
        const transcript = Array.from(event.results)
          .map(result => result[0])
          .map(result => result.transcript)
          .join('');

        if (event.results[0].isFinal) {
         this.transcriptions.unshift(transcript)
        }
      },
    },
    created() {
      this.startParrot()
    }
}
</script>

<style scoped>
  section {
    max-height: 95vh;
    overflow-y: auto;
  }

  section::-webkit-scrollbar {
    display: none;
  }

  h1 {
    margin: 0;
  }

</style>
