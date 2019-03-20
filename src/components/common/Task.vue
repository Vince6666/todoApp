<template>
  <div>
    <!-- 输入框 -->
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
      <span class="iconfont remove-icon" title="remove project" @click="removeProject">&#xe600;</span>
    </div>

    <!-- 列表项 -->
    <div class="task-list">
      <transition>
        <div v-show="showList">
          <div class="item"
              v-for="(item,index) of taskList"
              :key="index"
              :class="{'del-line': item.done}"
              v-show="currentActive === 'all' || (currentActive === 'active' && item.done === false) || (currentActive === 'completed' && item.done === true)  "
          >
            <input type="checkbox" class="check-box" v-model="item.done">
            {{item.content}}
            <button class="iconfont delete-item"
                    @click="deleteTaskItem(index)"
                    title="delete this item"
            >&#xe602;
            </button>
          </div>
        </div>
      </transition>
      <div class="task-manager" v-show="taskList.length">
        <span class="task-counter">{{leftItems}} items left</span>
        <ul>
          <li class="task-type" :class="{'task-active': currentActive == 'all'}" @click="showAll">all</li>
          <li class="task-type" :class="{'task-active': currentActive == 'active'}" @click="showActive">active</li>
          <li class="task-type" :class="{'task-active': currentActive == 'completed'}" @click="showCompleted">completed</li>
        </ul>
        <span class="task-clear" @click="clearCompleted">clear completed</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskInput',
  data () {
    return {
      inputValue: '',
      showList: true,
      currentActive: 'all',
      taskList: [
        // {
        //   content: 'vue',
        //   done: false
        // },
        // {
        //   content: 'react',
        //   done: false
        // },
        // {
        //   content: 'angular',
        //   done: false
        // }
      ]
    }
  },
  computed: {
    leftItems () {
      const leftItems = this.taskList.filter((val) => {
        return val.done === false
      })
      return leftItems.length
    }
  },
  methods: {
    chooseAll () {
      const allFinishedFlag = this.taskList.every((val) => {
        return val.done
      })
      if (allFinishedFlag) {
        this.taskList.forEach((val) => {
          val.done = false
        })
      } else {
        this.taskList.forEach((val) => {
          val.done = true
        })
      }
    },
    showAllItems () {
      this.showList = !this.showList
    },
    addTaskItem () {
      if (this.inputValue) {
        this.taskList.push({content: this.inputValue, done: false})
        this.inputValue = ''
      }
    },
    deleteTaskItem (index) {
      this.taskList.splice(index, 1)
    },
    showAll () {
      this.currentActive = 'all'
    },
    showActive () {
      this.currentActive = 'active'
    },
    showCompleted () {
      this.currentActive = 'completed'
    },
    clearCompleted () {
      this.taskList = this.taskList.filter((val) => {
        return val.done === false
      })
    },
    removeProject () {
      this.$emit('remove')
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
      &:hover
        background-color: #efefef
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
        float: left
      ul
        float: left
        line-height: 1.2rem
        height: 1.2rem
        .task-type
          float: left
          padding: .1rem .08rem
          margin: .24rem
          line-height: .48rem
          border: .02rem solid rgba(175, 47, 47, 0)
          &:hover
            cursor: pointer
            border-color: rgba(175, 47, 47, 0.3)
        .task-active
          background-color: rgba(175, 47, 47, 0.3)
          border: .02rem solid rgba(175, 47, 47, 0.3)
      .task-clear
        border: .02rem solid rgba(175, 47, 47, 0)
        padding: .16rem .12rem
        &:hover
          cursor: pointer
          border-color: rgba(175, 47, 47, 0.3)
</style>
