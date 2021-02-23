<template>
  <div>
      // Search input to filters produits
      <form>
          <span></span>
          <input v-model="query" type="search" placeholder="Search...">
      </form>

      // produit cards
      <div v-for="produit in filteredList" v-bind:key="produit">
          <div>
              <img :src="'http://localhost:1337/' + produit.image.id" alt="">
              <canvas width="600" height="400"></canvas>
          </div>
          <div>
              <div>
                  <h3>{{ produit.name }}</h3>
                  <p>{{ produit.description }}</p>
                  // Link to the produit using router-link
                  <router-link :to="{ name: 'produits-id', params: { id: produit.id }}" tag="a" class="uk-button uk-button-primary">See dishes
                  </router-link>
              </div>
          </div>
      </div>

      // If no produits have been found
      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <img src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
       <p>No produits found</p>
     </div>
  </div>
</template>

<script>
// Import the produits query
import produitsQuery from '~/apollo/queries/produit/produits'

export default {
  data() {
    return {
      // Initialize an empty produits variabkle
      produits: [],
      query: ''
    }
  },
  apollo: {
    produits: {
      prefetch: true,
      query: produitsQuery
    }
  },
  computed: {
    // Search system
    filteredList() {
      return this.produits.filter(produit => {
        return produit.name.toLowerCase().includes(this.query.toLowerCase())
      })
    },
  }
}
</script>