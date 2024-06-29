<script setup lang="ts">
import { useI18n, useSiteConfig } from '#imports'

const i18n = useI18n()

function setLanguage(code: string) {
  i18n.setLocale(code)
}

const locale = i18n.locale

const languageOptions = [
  [
    { label: 'English', click() { setLanguage('en') } },
    { label: 'French', click() { setLanguage('fr') } },
  ],
]

const siteConfig = useSiteConfig({
  name: 'Sitemap',
})
</script>

<template>
  <div class="flex min-h-screen flex-col">
    <header class="sticky top-0 z-50 w-full flex-none border-b border-gray-900/10 bg-white/75 backdrop-blur dark:border-gray-50/[0.06] dark:bg-gray-900/75">
      <UContainer class="py-3">
        <div class="flex items-center justify-between">
          <NuxtLink
            to="/"
            class="flex items-end gap-1.5 text-xl font-bold text-gray-900 dark:text-white"
          >
            <Icon
              name="logos:nuxt-icon"
              class="size-8"
            />
            Nuxt
            <div class="text-primary-500 dark:text-primary-400">
              {{ siteConfig.name }}
            </div>
          </NuxtLink>
          <UDropdown
            :items="languageOptions"
            :popper="{ placement: 'bottom-start' }"
          >
            <UButton
              color="white"
              :label="locale"
              trailing-icon="i-heroicons-chevron-down-20-solid"
            />
          </UDropdown>
        </div>
      </UContainer>
    </header>
    <main class="h-full min-h-full grow">
      <UContainer class="mt-4">
        <NuxtPage />
      </UContainer>
    </main>
    <footer class="flex items-center justify-center py-5 text-sm text-gray-700">
      Made by <UAvatar
        src="https://avatars.githubusercontent.com/u/5326365?v=4"
        size="xs"
        class="mx-1 size-5"
      /> Harlan Wilton
    </footer>
  </div>
</template>
