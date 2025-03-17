<script setup lang="ts">
import { object, string } from 'yup'

const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue', 'validate'])

const schema = object({
  contact_name: string().required('Contact Name is Required'),
  contact_email: string().email('Invalid Email').required('Email is Required'),
  contact_phone: string().required('Phone Number is Required'),
})

// Sync form state
const state = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})

// Validate only when in StepTwo
const validateForm = async () => {
  try {
    await schema.validate(state.value, { abortEarly: false })
    emit('validate', true) // Emit valid state only when in this step
  } catch (error) {
    emit('validate', false)
  }
}

// Validate only when the step is active
watch(state, validateForm, { deep: true })
</script>

<template>
  <UForm :schema="schema" :state="state" class="space-y-4">
    <UFormField label="Contact Name" name="contact_name" required>
      <UInput v-model="state.contact_name" />
    </UFormField>

    <UFormField label="Email" name="contact_email" required>
      <UInput v-model="state.contact_email" type="email" />
    </UFormField>

    <UFormField label="Phone Number" name="contact_phone" required>
      <UInput v-model="state.contact_phone" type="tel" />
    </UFormField>
  </UForm>
</template>
