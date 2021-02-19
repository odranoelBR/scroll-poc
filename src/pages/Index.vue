<template>
  <q-page class="q-pa-lg">
    <div class="row full-width full-height q-col-gutter-md">
      <div class="col">
        <q-input
          v-model="text"
          class="full-width full-height"
          filled
          type="textarea"
        />
      </div>
      <div class="col">
        scroll area here
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
      text
    }
  }
}
</script>
