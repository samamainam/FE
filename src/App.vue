<template>
  <div class="container">
    <div class="row">
      <div class="col-8">
        <ProductList />
      </div>
      <div class="col-4">
        <ScrapeProducts />
      </div>
    </div>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ScrapeProducts from "./components/Scrape-Products.vue";

export default {
  name: "App",
  components: { ScrapeProducts, ProductList },
};
</script>
