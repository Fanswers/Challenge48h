<template>
    <div class="container">
      <input v-model="query" class="form-control" type="text" placeholder="Search" aria-label="Search"/>
      <b-button variant="outline-primary m-3">Search</b-button>

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

      <div class="uk-container uk-container-center uk-text-center" v-if="filteredList.length == 0">
       <img src="https://assets-ouch.icons8.com/preview/19/52de2377-696e-4194-8c63-0a81aef60b4f.png" height="800" width="800">
       <p>No produits found</p>
     </div>
      <!--<div>
        <b-container fluid class="p-4">
          <b-row>
            <b-col>
              <b-img thumbnail fluid src="" alt="Image 1"></b-img>
            </b-col>
          </b-row>
        </b-container>
      </div>-->
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

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>