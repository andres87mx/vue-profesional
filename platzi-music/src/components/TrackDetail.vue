<template lang="pug">
  .container
    pm-loader(v-show="isLoading")
    .columns
      .column.is-5.is-offset-4
        pm-track(:track="track")
</template>
<script>
import TrackService from '@/services/track'
import PmTrack from '@/components/Track.vue'
import PmLoader from '@/components/shared/Loader.vue'
export default {
  components: { PmTrack, PmLoader },
  data () {
    return {
      track: {},
      showNotification: false,
      notify: {}
    }
  },
  created () {
    const id = this.$route.params.id
    this.isLoading = true
    TrackService.getById(id)
      .then(
        res => {
          this.track = res
          this.isLoading = false
        }
      )
  },
  watch: {
    showNotification () {
      if (this.showNotification) {
        setTimeout(() => {
          this.showNotification = false
        }, 3000)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
  .columns {
      margin: 20px;
  }
</style>
