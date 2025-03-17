<script setup lang="ts">
import StepOne from './StepOne.vue'
import { ref, reactive } from 'vue'

const items = [
  { id: 1, slot: 'business', title: 'Business Details' },
  { id: 2, slot: 'key', title: 'Key Contacts' },
  { id: 3, slot: 'profile', title: 'Business Profile' },
  { id: 4, slot: 'summary', title: 'Business Summary' },
  { id: 5, slot: 'declaration', title: 'Declaration Account' },
]

const stepper = useTemplateRef('stepper')
const currentStep = ref(1)
const isStepValid = ref(false) // Controls "Next" button

// Store form data globally (so it persists)
const formData = reactive({
  business_name: '',
  registration_date: '',
  renewal_date: '',
  expiry_date: '',
})

// Listen for validation updates
const handleValidation = (isValid: boolean) => {
  isStepValid.value = isValid
}

// Move to the next step
const nextStep = () => {
  if (isStepValid.value && stepper?.value?.hasNext) {
    stepper?.value?.next()
    currentStep.value++
  }
}

// Move to the previous step
const prevStep = () => {
  if (stepper?.value?.hasPrev) {
    stepper?.value?.prev()
    currentStep.value--
  }
}
</script>

<template>
  <div class="w-full">
    <UStepper disabled ref="stepper" :items="items">
      <template #content="{ item }">
        <div class="mx-auto">
          <StepOne v-if="item.id === 1" v-model="formData" @validate="handleValidation" />
        </div>
      </template>
    </UStepper>

    <div class="flex gap-2 justify-between mt-4">
      <UButton
        leading-icon="i-lucide-arrow-left"
        :disabled="!stepper?.hasPrev"
        @click="prevStep"
      >
        Prev
      </UButton>

      <UButton
        trailing-icon="i-lucide-arrow-right"
        :disabled="!isStepValid"
        @click="nextStep"
      >
        Next
      </UButton>
    </div>
  </div>
</template>
