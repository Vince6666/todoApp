<template>
  <div class="main">
    <todo-header @addNewProject="add"></todo-header>
    <task-input v-for="(item, index) of projectList" :key="index" @remove="removeSelf(index)"></task-input>
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
  },
  data () {
    return {
      projectList: [0],
      count: 0
    }
  },
  methods: {
    add () {
      this.projectList.push(this.count += 1)
    },
    removeSelf (index) {
      this.projectList = this.projectList.filter((val, num) => {
        return num !== index
      })
    }
  }
}
</script>

<style lang="stylus" scoped>
  .main
    width: 11rem
    margin: 0 auto
</style>
