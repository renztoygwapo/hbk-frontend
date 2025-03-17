<script setup>
useHead({ title: 'Submission Failed' })
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-red-100">
    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
      <div class="text-red-500">
        <i class="i-lucide-x-circle text-6xl"></i>
      </div>
      <h1 class="text-2xl text-red-500 font-bold mt-4">Submission Failed</h1>
      <p class="text-gray-600 mt-2">Oops! Something went wrong. Please try again later.</p>
      <UButton to="/" class="mt-4" color="primary">Go Home</UButton>
    </div>
  </div>
</template>
