<template>
  <div class="flex justify-center items-center min-h-screen bg-gray-100">
    <div class="container mx-auto px-4">
      <div class="text-center mb-8">
        <h1 class="text-3xl font-bold text-gray-800">Product List</h1>
      </div>
      <div v-if="products.length" class="grid md:grid-cols-3 gap-4">
        <div v-for="product in products" :key="product.id" class="bg-white p-4 shadow-lg rounded-lg">
          <div class="mb-2">
            <img :src="product.photo" alt="Product Image" class="max-h-40 w-full object-cover rounded">
          </div>
          <h2 class="text-xl font-bold mb-2">{{ product.name }}</h2>
          <p class="text-gray-600">{{ product.description }}</p>
          <div class="text-gray-700">Quantity: {{ product.quantity }}</div>
          <div class="text-gray-700">Price: ${{ product.price }}</div>
          <button @click="deleteProduct(product.id)" class="mt-4 bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded transition-colors duration-300 ease-in-out">
            Delete
          </button>
        </div>
      </div>
      <div v-else class="text-center text-gray-700">
        <p>No products have been added yet.</p>
      </div>
      <div class="mt-8 flex justify-center space-x-4">
        <nuxt-link to="/products/create" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded transition-colors duration-300 ease-in-out">Add Product</nuxt-link>   
        <nuxt-link to="/dashboard" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded transition-colors duration-300 ease-in-out">Home</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: []
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      this.products = JSON.parse(localStorage.getItem('products') || '[]');
    },
    deleteProduct(id) {
      this.products = this.products.filter(product => product.id !== id);
      localStorage.setItem('products', JSON.stringify(this.products));
    }
  }
}
</script>

<style scoped>
/* No additional styles needed with Tailwind in use */
</style>
