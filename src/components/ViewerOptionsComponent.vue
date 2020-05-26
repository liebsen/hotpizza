<template>
  <div class="column has-text-right">
    <div class="control">
      <div class="buttons levels has-addons">
        <button v-for="(item, index) in modes" :key="index" class="button is-rounded is-small" @click="setViewMode(item.name)" :class="{'has-background-success' : show === item.name}">
          <b-icon :icon="item.icon"/>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ViewerOptionsComponent',
  props: {
    show: {
      type: String,
      default: 'swipe'
    }
  },
  methods: {
    setViewMode (mode) {
      this.$emit('input', mode)
    }
  },
  data () {
    return {
      modes: [{
        name: 'swipe',
        icon: 'gesture-swipe-horizontal'
      }, {
        name: 'table',
        icon: 'view-list'
      }]
    }
  }
}
</script>
