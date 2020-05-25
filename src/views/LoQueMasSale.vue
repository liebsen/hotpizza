<template>
  <div>
    <title-bar :title-stack="titleStack"/>
    <section class="section is-main-section">
      <card-component title="Lo Que Mas Sale" class="has-table has-mobile-sort-spaced">
        <clients-table-sample :data-url="`${$router.options.base}data-sources/clients.json`"/>
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
  name: 'loquemassale',
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
        'Lo Que Mas Sale'
      ]
    }
  }
}
</script>
