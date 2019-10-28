<template lang="pug">
  #app
    .panel.is-primary
      .panel-heading Ejercicio de Manipulación del DOM by {{ name}}
      .panel-block
        .columns
          .column
            .box
              .field
                  p.is-size-3 New Task
              .field
                label.control Title:
                input.control(type="text", placeholder="Title", v-model="title")
              .field
                label.control Time
                input.control(type="numeric", placeholder="Time", v-model="time")
              .field
                button.button.is-info(@click="addTask") Add Task
                button.button.is-danger(@click="resetValues") Cancel
          .column
              .fieldset(v-if="tasks.length>0")
                p.is-size-5(v-show="totalTime") Horas trabajadas: {{ totalTime }}
                .columns
                  .column(v-for="(t, key) in tasks")
                    .box
                      p.is-size-7.has-text-weight-bold {{ t.title }}
                      p.is-size-7 {{ t.time}}
                      button.button.is-small(@click="removeTask(key)") Delete
              .fieldset(v-else)
                h1 No tasks yet!
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: 'ANDRES RUIZ',
      tasks: [],
      newTask: {},
      title: '',
      time: 0,
      existsTasks: false
    }
  },
  computed: {
    totalTime () {
      var time = 0
      for (let index = 0; index < this.tasks.length; index++) {
        time += parseInt(this.tasks[index].time)
      }
      return time
    }
  },
  created () {
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
  },
  methods: {
    addTask () {
      if ((this.title !== '') && (this.time > 0)) {
        this.tasks.push({
          title: this.title,
          time: this.time
        })
        alert('Added correctly!')
        this.resetValues()
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      } else {
        alert('Check your values!')
      }
    },
    resetValues () {
      this.title = ''
      this.time = 0
      this.newTask = {}
    },
    removeTask (key) {
      this.tasks.splice(key, 1)
      alert('Deleted correctly!')
      localStorage.setItem('tasks', JSON.stringify(this.tasks))
    }
  }
}
</script>

<style lang="scss">
  @import './scss/main.scss'
</style>
