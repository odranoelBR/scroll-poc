<template>
  <q-page
    class="q-pa-lg"
    @keydown.prevent.38="upSpeed"
    @keydown.prevent.40="downSpeed"
  >
    <div class="row full-width q-col-gutter-md justify-center">
      Here is the text we want to scroll
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
import { gsap } from "gsap";

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
    animationDurationTextHeight () {
      return this.$refs.text.clientHeight / 20
    }
  },
  mounted () {
    this.animate = gsap.fromTo(this.$refs.text,
      { y: '440px', ease: 'none' },
      { y: `-${this.textDivHeight}px`, duration: this.animationDurationTextHeight, ease: 'none' },
    );
    this.animate.pause()
    this.animate.onComplete = () => this.scrolling = false
  },
  methods: {
    startScrolling () {
      if (this.scrolling) {
        this.animate.pause()
        this.scrolling = false
      } else {
        this.animate.resume()
        this.scrolling = true
      }
    },
    upSpeed () {
      this.animate.timeScale(this.animate.timeScale() + 0.1)
    },
    downSpeed () {
      if (this.animate.timeScale() > 0.5) {
        this.animate.timeScale(this.animate.timeScale() - 0.1)
      }

    }
  }
}
</script>
<style >
.text {
  font-size: 4rem;
}
.text-container {
  height: 450px;
  overflow: hidden;
}
</style>