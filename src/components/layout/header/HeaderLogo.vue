<template>
  <router-link to="/">
    <div class="flex items-center justify-center rounded-lg overflow-hidden dark:bg-[#0f1929]">
      <img
        src="/images/logo/wave-logo_light.png"
        alt="Logo"
        class="dark:hidden h-10 w-auto"
      />
      <img
        src="/images/logo/wave-logo_dark.png"
        alt="Logo"
        class="hidden dark:block h-10 w-auto"
      />
    </div>
  </router-link>
</template>

<script setup lang="ts">
import { RouterLink } from 'vue-router'
</script>
