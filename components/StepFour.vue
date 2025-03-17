<script setup lang="ts">
const props = defineProps(['modelValue', 'currentStep'])
const emit = defineEmits(['update:modelValue', 'update:currentStep', 'submit'])

const state = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})

// Function to navigate back to a specific step
const editStep = (step) => {
  emit('update:currentStep', step)
}

// Submit the final form
const submitForm = () => {
  console.log("Final Submitted Data:", state.value)
  emit('submit', state.value)
}
</script>

<template>
  <div class="p-4 border rounded-lg shadow-lg space-y-4">
    <h2 class="text-lg font-semibold">Business Summary</h2>

    <div class="grid grid-cols-2 gap-4">
      <!-- Business Details -->
      <div>
        <h3 class="font-medium text-gray-600 flex justify-between">
          Business Details
          <UButton size="xs" color="gray" @click="editStep(1)">Edit</UButton>
        </h3>
        <p><strong>Business Name:</strong> {{ state.business_name }}</p>
        <p><strong>Registration Date:</strong> {{ state.registration_date }}</p>
        <p><strong>Renewal Date:</strong> {{ state.renewal_date }}</p>
        <p><strong>Expiry Date:</strong> {{ state.expiry_date }}</p>
      </div>

      <!-- Key Contacts -->
      <div>
        <h3 class="font-medium text-gray-600 flex justify-between">
          Key Contacts
          <UButton size="xs" color="gray" @click="editStep(2)">Edit</UButton>
        </h3>
        <p><strong>Contact Name:</strong> {{ state.contact_name }}</p>
        <p><strong>Email:</strong> {{ state.contact_email }}</p>
        <p><strong>Phone:</strong> {{ state.contact_phone }}</p>
      </div>

      <!-- Business Profile -->
      <div>
        <h3 class="font-medium text-gray-600 flex justify-between">
          Business Profile
          <UButton size="xs" color="gray" @click="editStep(3)">Edit</UButton>
        </h3>
        <p><strong>Business Type:</strong> {{ state.business_type }}</p>
        <p><strong>Annual Revenue:</strong> {{ state.annual_revenue }}</p>
        <p><strong>Number of Employees:</strong> {{ state.num_employees }}</p>
      </div>
    </div>

    <div class="flex justify-end mt-4">
      <UButton color="primary" @click="submitForm">
        Submit Final Form
      </UButton>
    </div>
  </div>
</template>
