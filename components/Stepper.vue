<script setup lang="ts">
const router = useRouter()

import StepOne from './StepOne.vue'
import StepTwo from './StepTwo.vue'
import StepThree from './StepThree.vue'
import StepFour from './StepFour.vue'
import { ref, reactive } from 'vue'

const items = [
  { id: 1, title: 'Business Details' },
  { id: 2, title: 'Key Contacts' },
  { id: 3, title: 'Business Profile' },
  { id: 4, title: 'Business Summary' },
]

const stepper = ref({ active: 0 }) 
const currentStep = ref(1)

const stepValidation = reactive({ 1: false, 2: false, 3: false })

// **🔹 Form Data**
const formData = reactive({
  business_name: '',
  registration_date: '',
  renewal_date: '',
  expiry_date: '',
  contact_name: '',
  contact_email: '',
  contact_phone: '',
  business_type: '',
  annual_revenue: '',
  num_employees: '',
})

// Handle step validation
const handleValidation = (step, isValid) => {
  stepValidation[step] = isValid
}

// Navigate through steps
const nextStep = () => {
  if (stepValidation[currentStep.value] && currentStep.value < items.length) {
    currentStep.value++
    stepper.value.active = currentStep.value - 1
  }
}
const prevStep = () => {
  if (currentStep.value > 1) {
    currentStep.value--
    stepper.value.active = currentStep.value - 1
  }
}
const goToStep = (step) => {
  currentStep.value = step
  stepper.value.active = step - 1
}

// **🔹 Submit Data to Backend**
const handleSubmit = async () => {
  try {
    const response = await $fetch('/api/submit-form', {
      method: 'POST',
      body: formData,
    })
    
    router.push('/success')
    console.log("Server Response:", response)
  } catch (error) {
    console.error("Submission Error:", error)
    router.push('/error')
  }
}
</script>

<template>
  <div class="w-full">
    <UStepper v-model="stepper.active" :items="items" disabled>
      <template #content="{ item }">
        <div class="mx-auto flex justify-center p-8">
          <StepOne v-if="item.id === 1" v-model="formData" @validate="(valid) => handleValidation(1, valid)" />
          <StepTwo v-if="item.id === 2" v-model="formData" @validate="(valid) => handleValidation(2, valid)" />
          <StepThree v-if="item.id === 3" v-model="formData" @validate="(valid) => handleValidation(3, valid)" />
          <StepFour v-if="item.id === 4" v-model="formData" :currentStep="currentStep" @update:currentStep="goToStep" @submit="handleSubmit" />
        </div>
      </template>
    </UStepper>

    <div class="flex gap-2 justify-between mt-4">
      <UButton leading-icon="i-lucide-arrow-left" :disabled="currentStep === 1" @click="prevStep">
        Prev
      </UButton>

      <UButton trailing-icon="i-lucide-arrow-right" v-if="currentStep < 4" :disabled="!stepValidation[currentStep]" @click="nextStep">
        Next
      </UButton>
    </div>
  </div>
</template>
