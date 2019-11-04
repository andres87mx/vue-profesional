<template lang="pug">
    section.hero.is-success
        .hero-head
            header.nav
                .container
                  .navbar
                    .navbar-brand
                      .navbar-item
                        strong Platzi Music 🎵
                    .navbar-end
                      .navbar-item
                        router-link.nav-item(to="/") Buscar
                      .navbar-item
                        router-link.nav-item(to="about") Nosotros
        .hero-body
            .container.has-text-centered
                h1.title Platzi Music
                h2.subtitle Canciones que estan buenisimas
                pm-player
</template>
<script>
import PmPlayer from '@/components/Player.vue'
export default {
  components: { PmPlayer }
}
</script>
