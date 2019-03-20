<template>
  <div>
    <p>Double-click to edit a todo</p>
    <p>This app is refered to <a href="https://gitee.com/Vince6666/TodoApp">origin</a></p>
    <p>Go to <a href="https://cn.vuejs.org/">vuejs.org</a></p>
  </div>
</template>

<script>
export default {
  name: 'InfoFooter'
}
</script>

<style lang="stylus" scoped>
  div
    margin-top: 1rem
    p
      text-align: center
      line-height: .6rem
      font-size: .36rem
      color: #ccc
      a
        color: #ccc
        text-decoration: none
        &:hover
          color: rgba(175,47,47,0.5)
</style>
