<template lang="pug">
  #app
    pm-header
    pm-notification(v-show="showNotification", :notification="notify")
      //- p(slot="body") No se encontraron resultados!
    pm-loader(v-show="isLoading")
    section.section(v-show="!isLoading")
      nav.nav
        .container
          input.input.is-large(type="text", placeholder="Buscar canciones", v-model="searchQuery")
          a.button.is-info.is-large(@click="search") Buscar
          a.button.is-dange.is-large &times;
      .container
        p
          small {{ searchMessage }}
      .container.results
        .columns.is-multiline
          .column.is-one-quarter(v-for="t in tracks")
            pm-track(:track="t", v-on:select="setSelectedTrack", v-bind:class="{ 'is-active': t.id == selectedTrack }")
    pm-footer
</template>

<script>
import trackService from '@/services/track'

import PmFooter from '@/components/layout/Footer.vue'
import PmHeader from '@/components/layout/Header.vue'

import PmTrack from '@/components/Track.vue'

import PmLoader from '@/components/shared/Loader.vue'
import PmNotification from '@/components/shared/Notification.vue'

export default {
  name: 'app',
  components: { PmFooter, PmHeader, PmTrack, PmLoader, PmNotification },
  data () {
    return {
      searchQuery: '',
      tracks: [],
      isLoading: false,
      selectedTrack: '',
      showNotification: false,
      notify: {}
    }
  },
  computed: {
    searchMessage () {
      return `Encontrados: ${this.tracks.length}`
    }
  },
  watch: {
    showNotification () {
      if (this.showNotification) {
        setTimeout(() => {
          this.showNotification = false
        }, 3000)
      }
    }
  },
  methods: {
    search () {
      if (!this.searchQuery) { return }
      this.isLoading = true
      trackService.search(this.searchQuery)
        .then(
          res => {
            if (res.tracks.total === 0) {
              this.notify = {
                message: 'Algo anduvo mal',
                type: 'is-danger'
              }
            } else {
              this.notify = {
                message: 'Se encontraron resultados',
                type: 'is-success'
              }
            }
            console.log(this.notify)
            this.showNotification = true
            this.tracks = res.tracks.items
            this.isLoading = false
          })
    },
    setSelectedTrack (id) {
      this.selectedTrack = id
    }
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss';
  .results {
    margin-top: 50px;
  }
  .is-active {
    border: 3px #23d160 solid;
  }
</style>
