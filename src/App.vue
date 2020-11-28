<template>
  <div id="app">
    <actual-page :premium="IsPremium"  @add-to-cart='hereaddToCart'></actual-page>
      <div class="cart">
         <p class="pcart">Cart ({{ cart.length }})</p>
      </div>
  </div>
</template>

<script>
import ActualPage from './components/ActualPage.vue'  

export default {
  name: 'App',
  components: {
    ActualPage,
  },
  data () {
    return {
      IsPremium: true,
      cart: [],
    }
  },
  methods: {
    hereaddToCart(id) {
      this.cart.push(id)
    }
  }
}
</script>

<style>
.pcart {
  position: absolute;
  right: 15%;
  top: 15%;
  border: 0.5px solid black;
  padding: 3px;
  font-size: 20px;
}
</style>
