<template>
  <q-page
    class="q-pa-lg"
    @keydown.prevent.38="upSpeed"
    @keydown.prevent.40="downSpeed"
  >
    <div class="row full-width q-col-gutter-md justify-center">
      here is the text we want to scroll
      <q-input
        v-model="text"
        class="full-width full-height"
        filled
        type="textarea"
      />
    </div>
    <div class="row q-mt-xl justify-center">
      <q-btn
        size="lg"
        :color="btnColor"
        :label="btnName"
        @click="startScrolling"
      />
    </div>
    <div class="row q-mt-xl justify-center bg-black text-container">
      <div
        ref="text"
        class="text-white text"
      >
        {{text}}
      </div>

    </div>
  </q-page>
</template>

<script>
import text from '../assets/text.js'

export default {
  name: 'PageIndex',
  data () {
    return {
      text,
      scrolling: false,
      duration: 5,
      animate: null
    }
  },
  computed: {
    btnName () {
      return this.scrolling ? 'Stop scrolling' : 'Start scrolling'
    },
    btnColor () {
      return this.scrolling ? 'negative' : 'primary'
    }
  },
  mounted () {
    this.animate = this.$refs.text.animate([
      // keyframes
      { transform: 'translateY(0px)' },
      { transform: `translateY(-${this.$refs.text.clientHeight}px)` }
    ], {
      // timing options
      duration: 5000
    });
    this.animate.pause()
    this.animate.onfinish = () => this.scrolling = false
  },
  methods: {
    startScrolling () {
      if (this.scrolling) {
        this.animate.pause()
        this.scrolling = false
      } else {
        this.scrolling = true
        this.animate.play()
      }
    },
    upSpeed () {
      this.animate.updatePlaybackRate(this.animate.playbackRate += 0.2)
    },
    downSpeed () {
      if (this.animate.playbackRate > 0.4) {
        this.animate.updatePlaybackRate(this.animate.playbackRate -= 0.2)
      }

    }
  }
}
</script>
<style scoped>
.text {
  font-size: 2rem;
  position: relative;
  overflow: hidden;
  bottom: -460px;
}
.text-container {
  height: 450px;
}
</style>