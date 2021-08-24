<template>
  <div id="wrapper">
    <nav class="navbar is-info">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item"><strong>Deli Greece</strong></router-link>

        <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
          <span aria-hidden="true"></span>
        </a>
      </div>

      <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu }">


        <div class="navbar-end">
          <router-link to="/oliveoil" class="navbar-item">Olive Oil</router-link>
          <router-link to="/honey" class="navbar-item">Honey</router-link>

          <div class="navbar-item">
            <div class="buttons">
              <router-link to="/log-in" class="button is-light">Log in</router-link>
              <router-link to="/cart" class="button is-success">
                <spam class="icon"><i class="fas fa-shoping-cart"></i> </spam>
                <spam>Cart ({{ cartTotalLength }})</spam>
              </router-link>
            </div>
          </div>
        </div>
      </div>
    </nav>

    <section class="section">
      <router-view/>
    </section>

  <footer class="footer">
      <p class="has-text-centered">Copyright (c) 2021</p>
  </footer>
    
  </div>
 
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return{
      showMobileMenu: false,
      cart: {
        items: []
      }
    }
  },
  beforeCreate() {
    this.$store.commit('initializeStore')
  },
  mounted() {
    this.cart = this.$store.state.cart
  },
  computed: {
    cartTotalLength() {
      let totalLength = 0

      for (let i = 0; i < this.cart.items.length; i++) {
        totalLength += this.cart.items[i].quantity
      }

      return totalLength
    }
  }
}
</script>

<style lang="scss">
@import '../node_modules/bulma'; 
</style>
