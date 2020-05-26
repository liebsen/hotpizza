<template>
<b-rate
    v-model="dataRate"
    :icon-pack="packs"
    :icon="icons"
    :max="maxs"
    :size="sizes"
    :show-score="score"
    :custom-text="custom"
    :show-text="text"
    :texts="texts"
    :rtl="isRtl"
    :spaced="isSpaced"
    :disabled="isDisabled">
  </b-rate>
</template>
<script>
export default {
  name: 'RateComponent',
  props: {
    dataRate: {
      type: Number,
      default: null
    }
  },
  data () {
    return {
      maxs: 5,
      sizes: '',
      packs: 'mdi',
      icons: 'pizza',
      score: true,
      custom: '',
      text: false,
      texts: ['Muy malo', 'Malo', 'Bueno', 'Muy Bueno', 'Excelente'],
      isRtl: false,
      isSpaced: false,
      isDisabled: true
    }
  }
}
</script>
