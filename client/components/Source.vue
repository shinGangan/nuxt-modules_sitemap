<script setup lang="ts">
import { joinURL } from 'ufo'
import type { SitemapSourceResolved } from '../../src/runtime/types'
import { data } from '../composables/state'

const props = defineProps<{ source: SitemapSourceResolved, showContext?: boolean }>()

const fetchUrl = computed(() => {
  const url = typeof props.source.fetch === 'string' ? props.source.fetch : props.source.fetch![0]
  if (url.includes('http'))
    return url
  return joinURL(data.value?.nitroOrigin || 'localhost', url)
})

function normaliseTip(tip: string) {
  // we need to convert code in the tip for example
  // this is `someCode` -> this is <code>someCode</code>
  return tip.replace(/`([^`]+)`/g, '<code>$1</code>')
}
</script>

<template>
  <OSectionBlock>
    <template #text>
      <div class="flex space-x-5">
        <h3 class="mb-1 flex items-center space-x-3 text-base opacity-80">
          <div
            v-if="source.fetch"
            class="flex space-x-2"
          >
            <NIcon
              icon="carbon:api-1"
              class="text-lg opacity-50"
            />
            <div
              v-if="source.timeTakenMs"
              class="text-sm opacity-60"
            >
              {{ source.timeTakenMs }}ms
            </div>
          </div>
          <div>
            {{ source.context.name }}
          </div>
          <div>
            <NBadge>{{ source.urls?.length || 0 }}</NBadge>
          </div>
        </h3>
      </div>
    </template>
    <template #description>
      <div class="flex items-center space-x-3">
        <div v-if="source.fetch">
          <NLink
            :href="fetchUrl"
            target="_blank"
          >
            {{ source.fetch }}
          </NLink>
        </div>
        <div
          v-if="source.context.description"
          class="mt-1 text-xs opacity-70"
        >
          {{ source.context.description }}
        </div>
      </div>
    </template>
    <div v-if="source.error">
      <NIcon
        icon="carbon:warning"
        class="text-red-500"
      /> {{ source.error }}
    </div>
    <OCodeBlock
      v-else
      class="max-h-[250px] overflow-y-auto"
      :code="JSON.stringify(source.urls, null, 2)"
      lang="json"
    />
    <div
      v-if="source.context.tips?.length"
      class="mt-2 bg-gray-50/50 p-3 opacity-70 dark:bg-gray-900/50"
    >
      <h3 class="mb-1 text-sm font-bold">
        Hints
      </h3>
      <ul class="ml-5 list-disc">
        <li
          v-for="(tip, key) in source.context.tips"
          :key="key"
          class="mb-1 text-sm opacity-80"
          v-html="normaliseTip(tip)"
        />
      </ul>
    </div>
  </OSectionBlock>
</template>
