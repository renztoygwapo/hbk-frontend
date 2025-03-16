<script setup lang="ts">
const items = [
  {
    slot: 'business',
    title: 'Business Details',
    icon: 'i-lucide-house'
  },
  {
    slot: 'key',
    title: 'Key Contacts',
    icon: 'i-lucide-truck'
  },
  {
    slot: 'profile',
    title: 'Business Profile',
  },
  {
    slot: 'key',
    title: 'Business Summary',
    icon: 'i-lucide-truck'
  },
  {
    slot: 'key',
    title: 'Declaration Account',
    icon: 'i-lucide-truck'
  },
]

const stepper = useTemplateRef('stepper')
</script>

<template>
  <div class="w-full">
    <UStepper ref="stepper" :items="items">
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
