<template>
    <div :class="['rounded-xl text-white shadow-lg p-5', bg]">
      <div class="flex items-center space-x-4">
        <div class="text-4xl">{{ icon }}</div>
        <div>
          <h2 class="text-lg font-semibold">{{ title }}</h2>
          <p class="text-2xl font-bold">{{ count }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'DashboardCard',
    props: {
      title: {
        type: String,
        required: true
      },
      count: {
        type: Number,
        required: true
      },
      icon: {
        type: String,
        required: true
      },
      bg: {
        type: String,
        default: 'bg-gray-500'
      }
    }
  }
  </script>

