<template>
  <div>
    <p>Double-click to edit a todo</p>
    <p>This app is refered to ...</p>
    <p>Go to <a href="">vuejs.org</a></p>
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
          color: pink
</style>
