<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <h1 class="mt-4">Scrape Products</h1>
        <h5 class="mt-4">*Enter Keyword to scrape Products from Search Page</h5>
        <input v-model="valueToSend" type="text" />
        <button @click="sendToBackend">Scrape Products</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import ProductList from "./ProductList.vue";

export default {
  data() {
    return {
      valueToSend: "",
      receivedValue: "",
    };
  },
  methods: {
    sendToBackend() {
      // Define the URL of your backend API
      const backendUrl = "http://localhost:3000/api/scrape-ebay";
      // Data to send to the backend
      const data = {
        value: this.valueToSend,
      };
      // Send a POST request to the backend
      axios
        .post(backendUrl, data)
        .then((response) => {
          this.receivedValue = response.data.value;
          // Handle the response from the backend if needed
          console.log("Backend response:", response.data);
        })
        .catch((error) => {
          // Handle any errors that occur during the request
          console.error("Error sending data to the backend:", error);
        });
    },
  },
  name: "App",
  components: {
    ProductList,
  },
};
</script>
