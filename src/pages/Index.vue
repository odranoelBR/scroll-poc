<template>
  <q-page class="q-pa-lg">
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
        color="primary"
        size="lg"
        label="start scrolling"
        @click="startScrolling"
      />
    </div>
    <div class="row q-mt-xl justify-center text-white">
      <q-scroll-area
        dark
        class="bg-dark text-white rounded-borders"
        style="height: 200px; max-width: 300px;"
      >
        <div
          v-for="n in 100"
          :key="n"
          class="q-py-sm q-px-md"
        >
          Lorem ipsum dolor sit amet, consectetur adipisicing
          elit, sed do eiusmod tempor incididunt ut labore et
          dolore magna aliqua.
        </div>
      </q-scroll-area>
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
      scrolling: null
    }
  },
  methods: {
    getYpos () {
      var ypos = this.$refs.text.offsetTop;
      var thisNode = this.$refs.text;
      while (thisNode.offsetParent && (thisNode.offsetParent != document.body)) {
        thisNode = thisNode.offsetParent;
        ypos += 0.5;
      }
      return ypos;
    },
    startScrolling () {
      if (this.scrolling) {
        window.clearTimeout(this.scrolling);
        this.scrolling = null;
      } else {
        this.doScroll();
      }
    },
    doScroll () {
      var y = parseInt(this.getYpos());
      this.styleTopNumber = y
      this.scrolling = window.setTimeout(this.doScroll, 200)
    },
  }
}
</script>
