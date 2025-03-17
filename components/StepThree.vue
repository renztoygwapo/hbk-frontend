<script setup lang="ts">
import { object, string, number } from 'yup'

const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue', 'validate'])

const schema = object({
  business_type: string().required('Business Type is Required'),
  annual_revenue: number().typeError('Annual Revenue must be a number').required('Annual Revenue is Required'),
  num_employees: number().typeError('Number of Employees must be a number').required('Number of Employees is Required'),
})

// Sync form state with Stepper
const state = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})

// Validate only when in StepThree
const validateForm = async () => {
  try {
    await schema.validate(state.value, { abortEarly: false })
    emit('validate', true) // Step is valid
  } catch (error) {
    emit('validate', false) // Step is invalid
  }
}

// Watch state to validate when changed
watch(state, validateForm, { deep: true })
</script>

<template>
  <UForm :schema="schema" :state="state" class="space-y-4">
    <UFormField label="Business Type" name="business_type" required>
      <UInput v-model="state.business_type" />
    </UFormField>

    <UFormField label="Annual Revenue" name="annual_revenue" required>
      <UInput v-model="state.annual_revenue" type="number" />
    </UFormField>

    <UFormField label="Number of Employees" name="num_employees" required>
      <UInput v-model="state.num_employees" type="number" />
    </UFormField>
  </UForm>
</template>
