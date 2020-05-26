<template>
  <div>
    <title-bar :title-stack="titleStack"/>
    <section class="section is-main-section">
      <viewer-options-component :show="show" @input="setVewMode"/>
      <swiper-component v-if="show === 'swipe'" :data-url="`${$router.options.base}data-sources/ofertas.json`"/>
      <card-component v-if="show === 'table'" title="Ofertas" class="has-table has-mobile-sort-spaced">
        <clients-table-sample :data-url="`${$router.options.base}data-sources/ofertas.json`"/>
      </card-component>
    </section>
  </div>
</template>

<script>
// @ is an alias to /src
import * as chartConfig from '@/components/Charts/chart.config'
import TitleBar from '@/components/TitleBar'
import CardComponent from '@/components/CardComponent'
import ClientsTableSample from '@/components/ClientsTableSample'
import SwiperComponent from '@/components/SwiperComponent'
import ViewerOptionsComponent from '@/components/ViewerOptionsComponent'
export default {
  name: 'ofertas',
  components: {
    ClientsTableSample,
    CardComponent,
    SwiperComponent,
    ViewerOptionsComponent,
    TitleBar
  },
  methods: {
    setVewMode (mode) {
      this.show = mode
    }
  },
  data () {
    return {
      show: 'swipe',
      defaultChart: {
        chartData: null,
        extraOptions: chartConfig.chartOptionsMain
      }
    }
  },
  computed: {
    titleStack () {
      return [
        'Ofertas'
      ]
    }
  }
}
</script>
