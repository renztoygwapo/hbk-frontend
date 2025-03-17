<script setup lang="ts">
import StepOne from './StepOne.vue';

const items = [
  {
    id: 1,
    slot: 'business',
    title: 'Business Details',
  },
  {
    id: 2,
    slot: 'key',
    title: 'Key Contacts',
  },
  {
    id: 3,
    slot: 'profile',
    title: 'Business Profile',
  },
  {
    id: 4,
    slot: 'key',
    title: 'Business Summary',
  },
  {
    id: 5,
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
          <div class="mx-auto">
            {{ item.id }}
            <StepOne v-if="item.id === 1" />
          </div>
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
