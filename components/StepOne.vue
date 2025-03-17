<script setup lang="ts">
import { boolean, object, string } from 'yup'

const props = defineProps(['modelValue'])
const emit = defineEmits(['update:modelValue', 'validate'])

const schema = object({
  business_name: string().required('Business Name is Required'),
  registration_date: string().required('Registration Date is Required'),
  renewal_date: string().required('Renewal Date is Required'),
  expiry_date: string().required('Expiration Date is Required'),
})

// Sync form state
const state = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})

// Validate form
const validateForm = async () => {
  try {
    await schema.validate(state.value, { abortEarly: false })
    emit('validate', true) // Emit valid state
  } catch (error) {
    emit('validate', false) // Emit invalid state
  }
}

// Watch for changes and revalidate
watch(state, validateForm, { deep: true })
</script>

<template>
  <UForm :schema="schema" :state="state" class="space-y-4">
    <UFormField label="Status">
      <USwitch v-model="state.status" />
    </UFormField>
    <UFormField label="Business Name" name="business_name" required>
      <UInput v-model="state.business_name" />
    </UFormField>

    <UFormField label="Registration Date" name="registration_date" required>
      <UInput v-model="state.registration_date" type="date" />
    </UFormField>

    <UFormField label="Expiry Date" name="expiry_date" required>
      <UInput v-model="state.expiry_date" type="date" />
    </UFormField>

    <UFormField label="Renewal Date" name="renewal_date" required>
      <UInput v-model="state.renewal_date" type="date" />
    </UFormField>
  </UForm>
</template>
