<template>
  <div class="M-CartControl" @click.stop="add"></div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'CartControl',
  methods: {
    add (event) {
      this.$emit('dropBall', event.target)
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .M-CartControl
    margin: 30px 0 0 30px
    width: 30px
    height: 30px
    background: #f00
</style>
