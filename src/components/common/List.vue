<template>
  <div class="task-list">
    <transition>
      <div v-show="showList">
        <div class="item"
              v-for="(item,index) of task_list"
              :key="index"
              :class="{'del-line': item.done}"
        >
          <input type="checkbox" class="check-box" v-model="item.done">
          {{item.content}}
          <button class="iconfont delete-item"
                  @click="deleteTaskItem(index)"
          >&#xe602;
          </button>
        </div>
      </div>
    </transition>  
    <div class="task-manager" v-show="task_list.length">
      <span class="task-counter">{{calcLeftTasks}} items left</span>
      <span class="task-type task-active">all</span>
      <span class="task-type" @click="showActiveTask">active</span>
      <span class="task-type">completed</span>
      <span class="task-type">clear completed</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    taskList: Array,
    showList: Boolean
  },
  data () {
    return {
      task_list: this.taskList,
      left_tasks: []
    }
  },
  computed: {
    calcLeftTasks () {
      this.left_tasks = []
      this.taskList.forEach((val, index) => {
        if (val.done === false) {
          this.left_tasks.push(val)
        }
      })
      return this.left_tasks.length
    }
  },
  methods: {
    deleteTaskItem (index) {
      this.taskList.splice(index, 1)
    },
    showActiveTask () {
      this.$emit('change')
    }
  }
}
</script>

<style lang="stylus" scoped>
  .v-enter, .v-leave-to
    opacity: 0
  .v-enter-active , .v-leave-active
    transition: .8s
  .task-list
    .item , .task-manager
      height: 1.2rem
      line-height: 1.2rem
      padding-left: .48rem
      font-size: .32rem
      border: .02rem solid #ccc
      box-sizing: border-box
      background-color: #fff
    .del-line
      text-decoration: line-through
      color: rgb(217, 217, 217)
    .item
      box-sizing: border-box
      position: relative
      height: 1.2rem
      line-height: .6rem
      font-size: .36rem
      padding: .32rem 1rem .32rem 1.36rem
      overflow: hidden
      white-space: nowrap
      text-overflow: ellipsis
      .check-box
        width: .42rem
        height: .42rem
        position: absolute
        top: .42rem
        left: .48rem
      .delete-item
        position: absolute
        line-height: .42rem
        border-radius: .21rem
        top: .42rem
        right: .32rem
        font-size: .42rem
        cursor: pointer
    .task-manager
      .task-counter
        margin-right: 1rem
      .task-type
        padding: .1rem .08rem
        margin-right: .48rem
        line-height: .48rem
        border: .02rem solid rgba(175, 47, 47, 0)
        &:hover
          cursor: pointer
          border-color: rgba(175, 47, 47, 0.3)
      .task-active
        background-color: rgba(175, 47, 47, 0.3)
        border: .02rem solid rgba(175, 47, 47, 0.3)
</style>