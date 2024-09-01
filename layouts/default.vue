import { Link } from '../.nuxt/components';
<template>
  <div class="container mx-auto max-w-2xl">
    <header class="flex justify-between items-center mt-5">
      <Logo />
      <Menu />
    </header>
    <main class="p-2">
      <slot />
    </main>
  </div>
</template>

<script lang="ts" setup>
useHead({
  titleTemplate: "%s - Abdelraouf Sabri",
  link: [
    {
      rel: "icon",
      type: "image/x-icon",
      href: "/favicon.ico",
    },
  ],
  htmlAttrs: {
    lang: "en",
  },
});
</script>

<style>
body {
  font-family: "Roboto", sans-serif;
}
</style>
