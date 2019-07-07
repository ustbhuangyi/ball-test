<template>
  <div class="Cart" ref="cart">
    <div class="ball-container">
      <div v-for="(ball,index) in balls" :key="index">
        <transition
          @before-enter="beforeDrop"
          @enter="dropping"
          @after-enter="afterDrop">
          <div class="ball" v-show="ball.show">
            <div class="inner inner-hook"></div>
          </div>
        </transition>
      </div>
    </div>
    <span>购物车</span>
  </div>
</template>

<script type="text/ecmascript-6">
export default {
  name: 'Cart',
  data () {
    return {
      balls: [
        {
          show: false
        },
        {
          show: false
        },
        {
          show: false
        },
        {
          show: false
        },
        {
          show: false
        }
      ],
      dropBalls: []
    }
  },
  methods: {
    drop (el) {
      for (let i = 0; i < this.balls.length; i++) {
        const ball = this.balls[i]
        if (!ball.show) {
          ball.show = true
          ball.el = el
          this.dropBalls.push(ball)
          return
        }
      }
    },
    beforeDrop (el) {
      const ball = this.dropBalls[this.dropBalls.length - 1]
      const rect = ball.el.getBoundingClientRect()
      const cartRect = this.$refs.cart.getBoundingClientRect()
      const x = -(cartRect.left - rect.left)
      const y = -(cartRect.top - rect.top)
      el.style.display = ''
      el.style.transform = el.style.webkitTransform = `translate3d(0,${y}px,0)`
      const inner = el.getElementsByClassName('inner-hook')[0]
      inner.style.transform = inner.style.webkitTransform = `translate3d(${x}px,0,0)`
    },
    dropping (el, done) {
      this._reflow = document.body.offsetHeight
      el.style.transform = el.style.webkitTransform = `translate3d(0,0,0)`
      const inner = el.getElementsByClassName('inner-hook')[0]
      inner.style.transform = inner.style.webkitTransform = `translate3d(0,0,0)`
      el.addEventListener('transitionend', done)
    },
    afterDrop (el) {
      const ball = this.dropBalls.shift()
      if (ball) {
        ball.show = false
        el.style.display = 'none'
      }
    }
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .Cart
    position: fixed
    right: 50px
    bottom: 50px
    width: 50px
    height: 50px
    line-height: 50px
    color: #fff
    text-align: center
    background: aqua
    border-radius: 50%

    .ball-container
      .ball
        position: absolute
        z-index: 200
        transition: all 0.5s cubic-bezier(0.49, -0.29, 0.75, 0.41)

        .inner
          width: 16px
          height: 16px
          border-radius: 50%
          background: blue
          transition: all 0.5s linear

</style>
