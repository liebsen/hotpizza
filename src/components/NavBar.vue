<template>
  <nav v-show="isNavBarVisible" id="navbar-main" class="navbar is-fixed-top">
    <div class="navbar-brand">
      <div class="logo">
        <router-link to="/">
          <img src="../assets/hplogo-icon.png" alt="HotPizza.me"/>
        </router-link>
      </div>
      <div class="navbar-item">
        <div class="control">
          <input class="input" placeholder="Buscar...">
        </div>
      </div>
    </div>
    <div class="navbar-brand is-right">
      <a class="navbar-item navbar-item-menu-toggle is-hidden-desktop" @click.prevent="menuNavBarToggle">
        <b-icon :icon="menuNavBarToggleIcon" size="is-medium"/>
      </a>
    </div>
    <div class="navbar-menu fadeIn animated faster" :class="{'is-active':isMenuNavBarActive}">
      <div class="navbar-end">
        <nav-bar-menu class="has-divider">
          <b-icon icon="menu" custom-size="default"/>
          <span>Menu</span>
          <div slot="dropdown" class="navbar-dropdown is-right">
            <router-link to="/promos" class="navbar-item" exact-active-class="is-active">
              <b-icon icon="account" custom-size="default"/>
              <span>Promos</span>
            </router-link>
            <router-link to="/ofertas" class="navbar-item">
              <b-icon icon="settings" custom-size="default"/>
              <span>Ofertas</span>
            </router-link>
            <router-link to="/revisiones" class="navbar-item">
              <b-icon icon="star" custom-size="default"/>
              <span>Revisiones</span>
            </router-link>
            <router-link to="/lo-que-mas-sale" class="navbar-item">
              <b-icon icon="pizza" custom-size="default"/>
              <span>Lo que más sale</span>
            </router-link>
          </div>
        </nav-bar-menu>
        <!--a href="https://justboil.me/bulma-admin-template/one" class="navbar-item has-divider is-desktop-icon-only" title="About">
          <b-icon icon="help-circle-outline" custom-size="default"/>
          <span>About</span>
        </a>
        <a class="navbar-item is-desktop-icon-only" title="Log out" @click="logout">
          <b-icon icon="logout" custom-size="default"/>
          <span>Log out</span>
        </a-->
      </div>
    </div>
  </nav>
</template>

<script>
import { mapState } from 'vuex'
import NavBarMenu from '@/components/NavBarMenu'

export default {
  name: 'NavBar',
  components: {
    NavBarMenu
  },
  data () {
    return {
      isMenuNavBarActive: false
    }
  },
  computed: {
    menuNavBarToggleIcon () {
      return (this.isMenuNavBarActive) ? 'close' : 'dots-vertical'
    },
    menuToggleMobileIcon () {
      return this.isAsideMobileExpanded ? 'backburger' : 'forwardburger'
    },
    ...mapState([
      'isNavBarVisible',
      'isAsideMobileExpanded',
      'userName'
    ])
  },
  methods: {
    menuToggleMobile () {
      this.$store.commit('asideMobileStateToggle')
    },
    menuNavBarToggle () {
      this.isMenuNavBarActive = (!this.isMenuNavBarActive)
    },
    logout () {
      this.$buefy.snackbar.open({
        message: 'Log out clicked',
        queue: false
      })
    }
  }
}
</script>
