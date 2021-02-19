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
      <q-btn color="primary" size="lg" label="start scrolling" @click="startScrolling" />
    </div>
    <div class="row q-mt-xl justify-center">
      show scrolling text here
    </div>
  </q-page>
</template>

<script>
import text from '../assets/text.js'

export default {
  name: 'PageIndex',
  data () {
    return {
      text
    }
  },
  methods: {
    startScrolling () {

    }
  }
}
</script>
