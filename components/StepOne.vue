<script setup lang="ts">
import { boolean, object, string, type InferType } from 'yup'
import type { FormSubmitEvent } from '@nuxt/ui'
import { CalendarDate, DateFormatter, getLocalTimeZone } from '@internationalized/date'


const status = ref(true)
const df = new DateFormatter('en-US', {
  dateStyle: 'medium'
})
// const registration_date = shallowRef(new CalendarDate(2025, 3, 18))
const expiry_date = shallowRef(new CalendarDate(2025, 3, 18))
const renewal_date = shallowRef(new CalendarDate(2025, 3, 18))

const schema = object({
  is_premium: string().required('This Field Required'),
  business_name: string().required('Business Name is Required'),
  registration_date: string().required('Registration Date is Required'),
  renewal_date: string().required('Renewal Date is Required'),
  expiry_date: string().required('Expiration Date is Required'),
})

type Schema = InferType<typeof schema>

const state = reactive({
  is_premium: true,
  business_name: undefined,
  registration_date: undefined,
  renewal_date: undefined,
  expiry_date: undefined,
})

const toast = useToast()
async function onSubmit(event: FormSubmitEvent<Schema>) {
  toast.add({ title: 'Success', description: 'The form has been submitted.', color: 'success' })
  console.log(event.data)
}
</script>

<template>
  <section class="flex justify-center w-full">
    <UForm :schema="schema" :state="state" class="space-y-4" @submit="onSubmit">
      <UFormField label="Business Name" name="business_name" required>
        <UInput v-model="state.business_name" label="Business Name"/>
      </UFormField>
      <UFormField label="Status">
      <USwitch v-model="status" />
    </UFormField>
    <UFormField name="is_premium">
      <UCheckbox v-model="state.is_premium" label="Is Company a Premium Company (with renewal exemption)" />
    </UFormField>
    <UFormField label="Accreditational Level">
      <UCheckbox label="Alumni Shield Level 1" />
      <UCheckbox label="Is Partially Accredited?" />
    </UFormField>
      <UFormField label="Registration Date" name="registration_date" required>
        <UPopover>
          <UButton color="neutral" variant="subtle" icon="i-lucide-calendar">
            {{ state.registration_date ? df.format(state.registration_date.toDate(getLocalTimeZone())) : 'Select a date' }}
          </UButton>

          <template #content>
            <UCalendar v-model="state.registration_date" class="p-2" />
          </template>
        </UPopover>
      </UFormField>
      <UFormField label="Expiry Date" name="expiry_date" required>
        <UPopover>
          <UButton color="neutral" variant="subtle" icon="i-lucide-calendar">
            {{ state.expiry_date ? df.format(state.expiry_date.toDate(getLocalTimeZone())) : 'Select a date' }}
          </UButton>

          <template #content>
            <UCalendar v-model="state.expiry_date" class="p-2" />
          </template>
        </UPopover>
      </UFormField>
      <UFormField label="Renewal Date" name="renewal_date" required>
        <UPopover>
          <UButton color="neutral" variant="subtle" icon="i-lucide-calendar">
            {{ state.renewal_date ? df.format(state.renewal_date.toDate(getLocalTimeZone())) : 'Select a date' }}
          </UButton>

          <template #content>
            <UCalendar v-model="state.renewal_date" class="p-2" />
          </template>
        </UPopover>
      </UFormField>
    <UButton type="submit">
      Submit
    </UButton>
  </UForm>
  </section>
</template>
