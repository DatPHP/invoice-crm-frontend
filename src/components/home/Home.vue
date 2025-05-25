<template>
    <div class="p-6 bg-gray-100 min-h-screen">
      <h1 class="text-3xl font-bold mb-6">Dashboard</h1>
      
      <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-6">
        <DashboardCard
          title="Total Categories"
          :count="categoryCount"
          icon="📁"
          bg="bg-blue-500"
        />
        <DashboardCard
          title="Total Products"
          :count="productCount"
          icon="📦"
          bg="bg-green-500"
        />
      </div>
    </div>
  </template>
  
<script>
import DashboardCard from './DashboardCard.vue'
import axios from "@/axios"; // Import the axios instance

export default {
  name: 'Home',
  components: {
    DashboardCard
  },
  data() {
    return {
      categoryCount: 0,
      productCount: 0
    }
  },
  methods: {
    async fetchCounts() {
      try {
        const response = await axios.get("/counts");
        const statistic_list = response.data;
        this.categoryCount = statistic_list?.data?.categories_count || 10;
        this.productCount = statistic_list?.data?.products_count || 10;
      } catch (error) {
        console.error("An error occurred while fetching the statistics:", error);
      }
    }
  },
  async created() {
    await this.fetchCounts();
  }
}
</script>
  