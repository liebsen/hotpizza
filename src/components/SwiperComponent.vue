<template>
  <div>
    <modal-box :is-active="isModalActive" :trash-object-name="trashObjectName" @confirm="trashConfirm" @cancel="trashCancel"/>
    <b-carousel v-show="data.length"
      :indicator="carousel.indicator"
      :indicator-background="carousel.indicatorBackground"
      :indicator-inside="carousel.indicatorInside"
      :indicator-mode="carousel.indicatorMode"
      :indicator-position="carousel.indicatorPosition"
      :indicator-style="carousel.indicatorStyle">
      <b-carousel-item v-for="(item, i) in data" :key="i">
        <section :class="`hero is-medium is-white`">
          <div class="hero-body has-text-centered">
            <div class="columns">
              <div class="column is-3 is-background-image" :style="`background-image: url('${item.image}')`">
              </div>
              <div class="column">
                <h1 class="title">{{item.name}}</h1>
                <h6>{{item.company}} {{item.address}}</h6>
                <rate-component :data-rate="item.rate"/>
              </div>
            </div>
          </div>
        </section>
      </b-carousel-item>
    </b-carousel>
    <section class="section" v-show="!data.length">
      <div class="content has-text-grey has-text-centered">
        <template v-if="isLoading">
          <p>
            <b-icon icon="dots-horizontal" size="is-large"/>
          </p>
          <p>Fetching data...</p>
        </template>
        <template v-else>
          <p>
            <b-icon icon="emoticon-sad" size="is-large"/>
          </p>
          <p>Nothing's here&hellip;</p>
        </template>
      </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios'
import ModalBox from '@/components/ModalBox'
import RateComponent from '@/components/RateComponent'
export default {
  name: 'SwiperComponent',
  components: {
    ModalBox,
    RateComponent
  },
  props: {
    dataUrl: {
      type: String,
      default: null
    },
    checkable: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      carousel: {
        indicator: true,
        indicatorBackground: true,
        indicatorInside: true,
        indicatorMode: 'hover',
        indicatorPosition: 'is-top',
        indicatorStyle: 'is-lines'
      },
      isModalActive: false,
      trashObject: null,
      data: [],
      isLoading: false,
      paginated: false,
      perPage: 10,
      checkedRows: []
    }
  },
  computed: {
    trashObjectName () {
      if (this.trashObject) {
        return this.trashObject.name
      }

      return null
    }
  },
  mounted () {
    if (this.dataUrl) {
      this.isLoading = true
      axios
        .get(this.dataUrl)
        .then(r => {
          this.isLoading = false
          if (r.data && r.data.data) {
            if (r.data.data.length > this.perPage) {
              this.paginated = true
            }
            this.data = r.data.data
          }
        })
        .catch(e => {
          this.isLoading = false
          this.$buefy.toast.open({
            message: `Error: ${e.message}`,
            type: 'is-danger'
          })
        })
    }
  },
  methods: {
    trashModal (trashObject) {
      this.trashObject = trashObject
      this.isModalActive = true
    },
    trashConfirm () {
      this.isModalActive = false
      this.$buefy.snackbar.open({
        message: 'Confirmed',
        queue: false
      })
    },
    trashCancel () {
      this.isModalActive = false
    }
  }
}
</script>
