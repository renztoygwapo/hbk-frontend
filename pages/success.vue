<script setup>
useHead({ title: 'Submission Successful' })
</script>

<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-green-100">
    <div class="bg-white p-6 rounded-lg shadow-lg text-center">
      <div class="text-green-500">
        <i class="i-lucide-check-circle text-6xl"></i>
      </div>
      <h1 class="text-2xl font-bold text-green-500 mt-4">Form Submitted Successfully!</h1>
      <p class="text-gray-600 mt-2">Thank you for your submission. We have received your data.</p>
      <UButton to="/" class="mt-4" color="primary">Go Home</UButton>
    </div>
  </div>
</template>
