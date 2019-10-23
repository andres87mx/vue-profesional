<template lang="pug">
  #app
    label(for="name") {{ 'Nombre' }}
    input(v-model="name")
    label(for="lastname") {{ 'Apellido' }}
    input(v-model="lastname")
    p {{'Nombre completo:' + fullname }}
    label(for="dia") {{ 'Dia:' }}
    input(v-model="dia" type="number")
    label(for="mes") {{ 'Mes:' }}
    input(v-model="mes" type="number")
    label(for="año") {{ 'Año:' }}
    input(v-model="año" type="number")
    p {{'Tu edad es de: ' + edad + ' Años'}}
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Hola desde vuejs!',
      name: '',
      lastname: '',
      dia: null,
      mes: null,
      año: null
    }
  },
  computed: {
    fullname () {
      return `${this.name} ${this.lastname}`
    },
    edad () {
      var hoy = new Date()
      var miFecha = new Date(this.año, this.mes, this.dia)
      var diff = hoy.getTime() - miFecha.getTime()
      return Math.floor(diff / (1000 * 60 * 60 * 24 * 365))
    }
  },
  watch: {
    name (newVal, oldVal) {
      console.log(newVal, oldVal)
    }
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss'
</style>
