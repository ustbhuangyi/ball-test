<template>
  <div class="home">
    <CartControl @dropBall="dropBall"></CartControl>
    <Cart ref="cart"></Cart>
  </div>
</template>

<script>
import Cart from '../components/Cart/Cart'
import CartControl from '../components/CartControl/CartControl'
export default {
  name: 'home',
  components: {
    Cart,
    CartControl
  },
  methods: {
    dropBall: function (target) {
      this.$refs.cart.drop(target)
    }
  }
}
</script>
