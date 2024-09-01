<template>
  <nav class="font-mono">
    <ul class="flex space-x-4">
      <li>
        <NuxtLink class="link" to="/">Home</NuxtLink>
      </li>
      <li>
        <NuxtLink class="link" to="/about">About</NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script lang="ts" setup></script>

<style>
.link {
  @apply p-1 font-mono hover:bg-gray-100;
}
</style>
