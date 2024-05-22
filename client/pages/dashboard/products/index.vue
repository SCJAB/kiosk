<template>
  <div class="scrollbar-hide">
    <div class="flex justify-center items-center h-screen bg-gray-100">
      <div class="container mx-auto px-4">
        <div class="text-center mb-8">
          <h1 class="text-3xl font-bold text-gray-800">Product List</h1>
        </div>
        <div v-if="products.length" class="">
          <div v-for="product in products" :key="product.id" class="bg-white p-4 shadow-lg rounded-lg flex justify-between">
            <div class="">
              <img :src="product.photo" alt="Product Image" class="max-h-16 w-32 object-cover rounded">
            </div>
            <div class=" w-full items-center flex ml-4">
              <h2 class="text-xl font-bold w-96">{{ product.name }}</h2>
              <p class="text-gray-600 w-72">{{ product.description }}</p>
              <div class="text-gray-700 w-48">Quantity: {{ product.quantity }}</div>
              <div class="text-gray-700 w-48">Price: ${{ product.price }}</div>
              <div class="flex justify-end items-center w-48">
                <button @click="updateProduct(product.id)" class="bg-[#fff019] hover:bg-[#fffab8] text-[#1B5D88] font-bold py-2 px-4 mx-1 rounded transition-colors duration-300 ease-in-out">Update</button>
                
              </div>  
            </div>
          </div>
        </div>
        <div v-else class="text-center text-gray-700">
          <p>No products have been added yet.</p>
        </div>
        <div class="mt-8 flex justify-center space-x-4">
          <nuxt-link to="/dashboard/products/create" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded transition-colors duration-300 ease-in-out">Add Product</nuxt-link>   
          <nuxt-link to="/dashboard" class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded transition-colors duration-300 ease-in-out">Home</nuxt-link>
        </div>
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
    updateProduct(id) {
      this.$router.push({ path: `/products/update/${id}` });
    }
  }
}
</script>

<style scoped>
/* No additional styles needed with Tailwind in use */
</style>
