<template lang="pug">
  #app
    section.section
      .container
        label {{ name }}
      .container
        label tasks
    
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: '',
      task: [1, 2, 3, 4, 5]
    }
  },
  computed: {
  },
  watch: {
  },
  methods: {
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss'
</style>
