<script setup lang="ts">
import { definePageMeta } from '#imports'

// does not work (yet?)
definePageMeta({
  sitemap: {
    changefreq: 'daily',
  },
})
</script>

<template>
  <div>
    <h1 class="mb-5 mt-10 text-2xl">
      Sitemap
    </h1>
    <div class="mx-auto grid max-w-[900px] grid-cols-2 gap-5">
      <NuxtLink to="/ignore-foo">
        ignore-foo
      </NuxtLink>
      <NuxtLink to="/new-page">
        new page
      </NuxtLink>
      <NuxtLink to="/about">
        about
      </NuxtLink>
      <NuxtLink to="/secret">
        secret
      </NuxtLink>
      <NuxtLink to="/users-prerender">
        dynamic pre-render link
      </NuxtLink>
      <NuxtLink to="/blog">
        blog
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped>
a {
  display: block;
  margin: 0 0 10px 0;
  text-decoration: underline;
}
</style>
