<template>
  <div>
    <modal-box :is-active="isModalActive" :trash-object-name="trashObjectName" @confirm="trashConfirm"
               @cancel="trashCancel"/>
    <b-table
      :checked-rows.sync="checkedRows"
      :checkable="checkable"
      :loading="isLoading"
      :paginated="paginated"
      :per-page="perPage"
      :striped="true"
      :hoverable="true"
      default-sort="name"
      :data="clients">

      <template slot-scope="props">
        <b-table-column class="has-no-head-mobile is-image-cell">
          <div class="image">
            <img :src="props.row.avatar" :alt="props.row.name" class="is-rounded">
          </div>
        </b-table-column>
        <b-table-column label="Nombre" field="name" sortable>
          {{ props.row.name }}
        </b-table-column>
        <b-table-column label="Comercio" field="company" sortable>
          {{ props.row.company }}
        </b-table-column>
        <b-table-column label="Ubicación" field="city" sortable>
          {{ props.row.city }}
        </b-table-column>
        <b-table-column class="is-progress-col" label="Calificación" field="rate" sortable>
          <rate-component :data-rate="props.row.rate">
          </rate-component>
        </b-table-column>
        <b-table-column label="Precio">
          <small class="has-text-grey is-abbr-like" :title="props.row.created">{{ props.row.price }} ARS</small>
        </b-table-column>
        <b-table-column custom-key="actions" class="is-actions-cell">
          <div class="buttons is-right">
            <router-link :to="{name:'client.edit', params: {id: props.row.id}}" class="button is-medium is-success is-rounded is-outlined">
              <b-icon icon="cart-arrow-down" size="is-medium"/>
            </router-link>
            <button class="button is-medium is-danger is-rounded is-outlined" type="button" @click.prevent="trashModal(props.row)">
              <b-icon icon="cart-remove" size="is-medium"/>
            </button>
          </div>
        </b-table-column>
      </template>

      <section class="section" slot="empty">
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
    </b-table>
  </div>
</template>

<script>
import axios from 'axios'
import ModalBox from '@/components/ModalBox'
import RateComponent from '@/components/RateComponent'
export default {
  name: 'ClientsTableSample',
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
      isModalActive: false,
      trashObject: null,
      clients: [],
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
            this.clients = r.data.data
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
