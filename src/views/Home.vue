<template>
  <div class="is-landing">
    <div class="columns is-vcentered has-text-centered">
      <div class="column">
        <router-link to="/productos" class="button is-white is-outlined is-rounded is-large">
          <span>Productos</span>
        </router-link>
        <router-link to="/ofertas" class="button is-white is-outlined is-rounded is-large">
          <span>Ofertas</span>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
export default {
  name: 'home',
  data () {
    return {
    }
  },
  mounted () {
    this.$buefy.snackbar.open({
      message: 'Welcome back',
      queue: false
    })
  }
}
</script>
