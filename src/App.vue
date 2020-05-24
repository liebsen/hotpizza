<template>
  <div id="app">
    <nav-bar/>
    <router-view/>
    <footer-bar/>
  </div>
</template>

<script>
// @ is an alias to /src
import NavBar from '@/components/NavBar'
import FooterBar from '@/components/FooterBar'

export default {
  name: 'home',
  components: {
    FooterBar,
    NavBar
  },
  computed: {
    menu () {
      return [
        'General',
        [
          {
            to: '/',
            icon: 'desktop-mac',
            label: 'Inicio'
          }
        ],
        'Examples',
        [
          {
            to: '/ofertas',
            label: 'Ofertas',
            icon: 'table',
            updateMark: true
          },
          {
            to: '/productos',
            label: 'Productos',
            icon: 'square-edit-outline'
          }
        ],
        'Nosotros',
        [
          {
            to: '/nosotros',
            label: 'Sobre Nosotros',
            icon: 'credit-card'
          },
          {
            to: '/contacto',
            label: 'Contacto',
            icon: 'credit-card'
          }
        ]
      ]
    }
  }
}
</script>
