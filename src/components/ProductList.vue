<template>
  <div class="container">
    <h1 class="mt-4">Product List</h1>
    <div class="row">
      <div class="col-12 mb-3">
        <ProductFilter @search="handleSearch" />
      </div>
    </div>
    <div class="row">
      <div class="col-12">
        <div v-if="loading" class="text-center mt-4">Loading...</div>
        <div v-else>
          <div
            class="card mb-3"
            v-for="product in filteredProducts"
            :key="product.id"
          >
            <div class="row no-gutters">
              <div class="col-md-4">
                <img
                  :src="product.image_url"
                  class="card-img"
                  :alt="product.product_name"
                />
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{ product.product_name }}</h5>
                  <p class="card-text">Price: {{ product.price }}</p>
                  <a :href="product.link" class="btn btn-primary"
                    >View on eBay</a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductFilter from "./ProductFilter.vue";

export default {
  components: {
    ProductFilter,
  },
  data() {
    return {
      products: [],
      filteredProducts: [], // Filtered products to display
      loading: true,
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      axios
        .get("http://localhost:3000/api/products")
        .then((response) => {
          this.products = response.data;
          this.filteredProducts = response.data;
          this.loading = false;
        })
        .catch((error) => {
          console.error(error);
          this.loading = false;
        });
    },
    handleSearch(searchQuery) {
      if (searchQuery.trim() === "") {
        // If the search query is empty, show all products
        this.filteredProducts = this.products;
      } else {
        // Filter products based on the search query
        this.filteredProducts = this.products.filter((product) =>
          product.product_name.toLowerCase().includes(searchQuery.toLowerCase())
        );
      }
    },
  },
};
</script>

<!-- 

<template>
  <div class="container">
    <h1 class="mt-4">Product List</h1>
    <div class="row">
      <div class="col-12">
        <div v-if="loading" class="text-center mt-4">Loading...</div>
        <div v-else>
          <div class="card mb-3" v-for="product in products" :key="product.id">
            <div class="row no-gutters">
              <div class="col-md-4">
                <img
                  :src="product.image_url"
                  class="card-img"
                  :alt="product.product_name"
                />
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{ product.product_name }}</h5>
                  <p class="card-text">Price: {{ product.price }}</p>
                  <a :href="product.link" class="btn btn-primary"
                    >View on eBay</a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      products: [],
      loading: true,
    };
  },
  mounted() {
    axios
      .get("http://localhost:3000/api/products") // Change the URL to match your backend server
      .then((response) => {
        this.products = response.data;
        this.loading = false;
      })
      .catch((error) => {
        console.error(error);
        this.loading = false;
      });
  },
};
</script> -->
