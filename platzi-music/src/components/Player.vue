<template lang="pug">
    .content(v-if="track && track.album")
      p.is-128x128
        img(:src="track.album.images[0].url")
      p
        strong {{ track.name }}
        small [{{ track.duration_ms | ms-to-mn }}]
      p(v-if="track.preview_url")
        audio(controls, :src="track.preview_url")
      p(v-else)
        strong Sin preview de cancion.
</template>
<script>
import { mapState } from 'vuex'
export default {
  computed: {
    ...mapState(['track'])
  }
  /* data () {
    return {
      track: {}
    }
  },
  created () {
    this.$bus.$on('set-track', (track) => {
      this.track = track
    })
  } */
}
</script>
<style lang="scss">
  img {
    width: 124px;
    border-radius: 50%;
  }
</style>
