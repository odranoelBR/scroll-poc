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
        v-html="text"
      />

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
      animate: null
    }
  },
  computed: {
    btnName () {
      return this.scrolling ? 'Stop scrolling' : 'Start scrolling'
    },
    btnColor () {
      return this.scrolling ? 'negative' : 'primary'
    },
    textDivHeight () {
      return this.$refs.text.clientHeight
    },
    animateDurationBasedOnTextHeight () {
      return this.$refs.text.clientHeight * 15
    }
  },
  mounted () {
    this.animate = this.$refs.text.animate([
      // keyframes
      { transform: 'translateY(500px)' },
      { transform: `translateY(-${this.textDivHeight}px)` }
    ], {
      duration: this.animateDurationBasedOnTextHeight
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
        this.animate.play()
        this.scrolling = true
      }
    },
    upSpeed () {
      if (this.animate.playbackRate < 3) {
        this.animate.updatePlaybackRate(this.animate.playbackRate += 0.05)
      }
    },
    downSpeed () {
      if (this.animate.playbackRate > 0.4) {
        this.animate.updatePlaybackRate(this.animate.playbackRate -= 0.1)
      }
    }
  }
}
</script>
<style >
.text {
  font-size: 4rem;
  animation-fill-mode: both;
  z-index: 1;
  will-change: scroll-position;
}
.text-container {
  height: 450px;
  overflow: hidden;
}
</style>