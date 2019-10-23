<template lang="pug">
  #app
    h1 CURSO PROFESIONAL VUEJS
    hr
    h2 EXPRESIONES
    p {{ 1 + 1 }}
    p {{ 'Hola' + 'Mundo' }}
    p {{ person.name }}
    p {{ person.name.toUpperCase() }}
    p {{ JSON.stringify(person) }}
    p {{ true ?'true':'false'}}
    hr
    h2 DIRECTIVAS
    p(v-show="showValue") {{ value }}
    p(v-if="showValue") {{ value }}
    p(v-else-if="false") {{ 'algo mas' }}
    p(v-else) {{ 'lo ultimo' }}
    ul
      li(v-for="i in items") {{ i }}
    hr
    h2 DATA BINDING
    input(v-model="name")
    p {{ name }}
    a(:href="url") Link
    hr
    h2 COMPUTED PROPERTIES
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
    hr
    h2 WATCHERS
    label {{ 'Usar input name y ver consola navegador' }}
    hr
    h2 EVENTOS
    label(for="variable") {{ 'Variable' }}
    input(v-model="variable")
    button(:click="format") Formatear
    p {{ formattedVariable }}
    hr
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Hola desde vuejs!',
      person: {
        name: 'Andrés'
      },
      showValue: false,
      value: 'Algo',
      items: [1, 2, 3, 4, 5],
      name: '',
      url: 'https://platzi.com',
      lastname: '',
      dia: null,
      mes: null,
      año: null,
      variable: '',
      formattedVariable: ''
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
  },
  methods: {
    format () {
      this.formattedVariable = this.variable.split(' ').join('-')
    }
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss'
</style>
