<template>
  <div>
    <div class="task">
      <span class="iconfont arrow-down"
            title="choose all item"
            @click="chooseAll"
      >&#xe62d;
      </span>
      <input type="text" class="add-task" placeholder="请输入待办事项"
             v-model="inputValue"
             @keyup.enter="addTaskItem"
      >
      <button class="task-button" @click="showAllItems">点击隐藏或显示</button>
      <span class="iconfont remove-icon" title="remove project">&#xe600;</span>
    </div>
    <task-list :showList="showList" :taskList="taskList" @change="changeTaskList"></task-list>
  </div>
</template>

<script>
import TaskList from './List'
export default {
  name: 'TaskInput',
  components: {
    TaskList
  },
  data () {
    return {
      inputValue: '',
      leftTasks: [],
      showList: true,
      taskList: [
        {
          content: 'vue',
          done: false
        },
        {
          content: 'react',
          done: false
        },
        {
          content: 'angular',
          done: false
        }
      ]
    }
  },
  methods: {
    chooseAll () {
      this.taskList.forEach((val) => {
        val.done = true
      })
    },
    showAllItems () {
      this.showList = !this.showList
    },
    addTaskItem () {
      this.taskList.push({content: this.inputValue, done: false})
      this.inputValue = ''
    },
    changeTaskList () {
      const newList = []
      this.taskList.forEach((val) => {
        if (val.done === false) {
          newList.push(val)
        }
      })
      this.taskList = newList
      console.log(this.taskList)
    }
  }
}
</script>

<style lang="stylus" scoped>
  .task
    position: relative
    .arrow-down
      position: absolute
      left: .56rem
      top: .32rem
      padding: .12rem
      border-radius: .12rem
      color: #666
      &:hover
        background-color: pink
        cursor: default
    .add-task
      width: 100%
      height: 1.2rem
      padding: .32rem 2.6rem .32rem 1.36rem
      font-size: .5rem
      border: .02rem solid #ccc
      box-sizing: border-box
      background-color #f5f5f5
    .task-button
      position: absolute
      right: .32rem
      top: 0.34rem
      background-color: #ddd
      border-radius: .12rem
      padding: .06rem
      color: #666
      &:hover
        background-color: rgba(175, 47, 47, 0.3)
    .remove-icon
      position: absolute
      right: -0.8rem
      top: .34rem
      font-size: .5rem
      cursor: pointer
</style>