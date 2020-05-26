<template>
  <div class="is-landing">
    <div class="columns is-vcentered has-text-centered is-hidden-mobile">
      <div class="column ">
        <router-link to="/ofertas" class="button is-white is-outlined is-rounded is-large">
          <span>Ofertas</span>
        </router-link>
        <router-link to="/promos" class="button is-white is-outlined is-rounded is-large">
          <span>Promos</span>
        </router-link>
      </div>
    </div>
    <div class="columns is-vcentered has-text-centered is-hidden-tablet">
      <div class="column">
        <router-link to="/ofertas" class="button is-white is-outlined is-rounded is-large">
          <span>Ofertas</span>
        </router-link>
      </div>
      <div class="column">
        <router-link to="/promos" class="button is-white is-outlined is-rounded is-large">
          <span>Promos</span>
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
  }
}
</script>
