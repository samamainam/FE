<template>
  <div>
    <input
      v-model="searchQuery"
      @input="performSearch"
      class="form-control"
      type="text"
      placeholder="Search by product title..."
    />
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
    };
  },
  methods: {
    performSearch() {
      this.$emit("search", this.searchQuery);
    },
  },
};
</script>
