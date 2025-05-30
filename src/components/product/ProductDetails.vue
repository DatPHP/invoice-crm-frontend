<template>
  <!-- Product details container -->
  <!-- Use Vue's 'v-if' directive to render this container only if 'product' is truthy -->
  <!--This is like a magic switch. If we have a toy car (product details), the stand lights up and shows the toy. If not, it stays empty.-->
  <div v-if="product" class="product-details">
    <!-- Display the product name -->
    <h2 class="product-title">{{ product.name }}</h2>
    <!-- Display the product description -->
    <p class="product-description">{{ product.description }}</p>
    <!-- Display the product price -->
    <p class="product-price">Price: ${{ product.price }}</p>
    
    <!-- Display the product category -->
    <p class="product-category">Category: {{ product?.category?.category_name }}</p>

    <div class="flex justify-center items-center">
      <img v-if="product.image"
      :src="`http://localhost:8000/storage/product/image/${product.image}`"
      alt="Product Image">

      <img v-if="!product.image"
      src="https://docs.material-tailwind.com/img/logos/logo-spotify.svg"
      alt="Spotify"
      class="relative inline-block h-12 w-12 !rounded-full border border-blue-gray-50 bg-blue-gray-50/50 object-contain object-center p-1"
      >
    </div>

  </div>
</template>

<script>
import axios from "@/axios"; // Import the axios instance

export default {
  // Component data
  data() {
    return {
      // Initialize product as null
      product: null, // This means our box is empty to start with
      // Initialize categories array
      categories: [],
    };
  },
  // Lifecycle hook that is called after the instance has been mounted
  async mounted() {
    // the component being ready and visible in the browser for the first time.then
    // we immediately fetch and display the product details.(after that component can update and re-render as many times as needed based on data changes or other interactions.)
    // Get the product ID from the route params
    const productId = this.$route.params.id; // This is like a magic number that tells us which toy car we want. Maybe it's toy car number 5 or number 10
    try {
      // Fetch categories first
      const categoriesResponse = await axios.get("/categories");
      this.categories = categoriesResponse.data;

      // Then fetch the product data
      const response = await axios.get(`/products/${productId}`);
      this.product = response.data;
    } catch (error) {
      // If an error occurs, log it to the console
      console.error("An error occurred while fetching the data:", error);
    }
  },
  computed: {
    // Computed property to get the category name
    categoryName() {
      if (!this.product || !this.product.category_id) return 'Uncategorized';
      const category = this.categories.find(cat => cat.id === this.product.category_id);
      return category ? category.category_name : 'Uncategorized';
    }
  },
};
</script>

<style scoped>
.product-details {
  max-width: 600px;
  margin: 20px auto;
  padding: 20px;
  background-color: #f9f9f9;
  border-radius: 8px;
}

.product-title {
  margin-bottom: 20px;
  font-size: 2em;
}

.product-description {
  font-size: 1.2em;
}

.product-price {
  margin-top: 20px;
  font-size: 1.2em;
  font-weight: bold;
}

.product-category {
  margin-top: 10px;
  font-size: 1.1em;
  color: #666;
}
</style>
