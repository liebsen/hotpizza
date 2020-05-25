<template>
  <div>
    <title-bar :title-stack="titleStack"/>
    <section class="section is-main-section">
      <card-component title="Ofertas" class="has-table has-mobile-sort-spaced">
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
export default {
  name: 'ofertas',
  components: {
    ClientsTableSample,
    CardComponent,

    TitleBar
  },
  data () {
    return {
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
