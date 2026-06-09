<template>
  <div class="app-wrapper">
    <Tasks />
    <hr class="divider" />
    <Task2 @toggle-dark="toggleDark" :is-dark="isDark" />
    <hr class="divider" />
    <Task3 />
  </div>
</template>

<script>
import Tasks from './components/tasks.vue'
import Task2 from './components/task2.vue'
import Task3 from './components/task3.vue'

export default {
  name: 'App',
  components: { Tasks, Task2, Task3 },
  data() {
    return {
      isDark: false
    }
  },
  methods: {
    toggleDark() {
      this.isDark = !this.isDark
      document.body.classList.toggle('dark-mode', this.isDark)
    }
  }
}
</script>