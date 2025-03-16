<script setup lang="ts">
const items = [
  {
    slot: 'business',
    title: 'Business Details',
  },
  {
    slot: 'key',
    title: 'Key Contacts',
  },
  {
    slot: 'profile',
    title: 'Business Profile',
  },
  {
    slot: 'key',
    title: 'Business Summary',
  },
  {
    slot: 'key',
    title: 'Declaration Account',
  },
]

const stepper = useTemplateRef('stepper')
</script>

<template>
  <div class="w-full">
    <UStepper disabled ref="stepper" :items="items">
      <template #content="{ item }">
        <Placeholder class="aspect-video">
          {{ item.title }}
        </Placeholder>
      </template>
    </UStepper>

    <div class="flex gap-2 justify-between mt-4">
      <UButton
        leading-icon="i-lucide-arrow-left"
        :disabled="!stepper?.hasPrev"
        @click="stepper?.prev()"
      >
        Prev
      </UButton>

      <UButton
        trailing-icon="i-lucide-arrow-right"
        :disabled="!stepper?.hasNext"
        @click="stepper?.next()"
      >
        Next
      </UButton>
    </div>
  </div>
</template>
