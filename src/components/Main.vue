<template>
  <div class="main">
    <todo-header></todo-header>
    <task-input></task-input>
    <info-footer></info-footer>
  </div>
</template>

<script>
import todoHeader from './common/Header'
import InfoFooter from './common/Footer'
import TaskInput from './common/Task'
export default {
  name: 'Main',
  components: {
    todoHeader,
    InfoFooter,
    TaskInput
  }
}
</script>

<style lang="stylus" scoped>
  .main
    width: 11rem
    margin: 0 auto
</style>
