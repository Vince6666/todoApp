<template>
  <div class="title-container">
    <h1 class="title">todoApp</h1>
    <span class="iconfont add-icon" title="add a new project" @click="addProject">&#xe601;</span>
  </div>
</template>

<script>
export default {
  name: 'todoHeader',
  methods: {
    addProject () {
      this.$emit('addNewProject')
    }
  }
}
</script>

<style lang="stylus" scoped>
  .title-container
    position: relative
    .title
      font-size: 2rem
      color: rgba(175, 47, 47, .5)
      text-align: center
      margin: 1rem 0 .8rem 0
    .add-icon
      position: absolute
      right: -0.84rem
      top: .86rem
      font-size: .6rem
      cursor: pointer
</style>
