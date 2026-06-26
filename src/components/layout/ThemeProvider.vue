<template>
  <slot></slot>
</template>

<script setup lang="ts">
import { ref, provide, onMounted, watch, computed } from 'vue'

const theme = ref<Theme>('light')
const isInitialized = ref(false)

const currentTheme = computed(() => theme.value)

const isDarkMode = computed(() => {
  if (theme.value === 'system') {
    return window.matchMedia('(prefers-color-scheme: dark)').matches
  }
  return theme.value === 'dark'
})

const setTheme = (newTheme: Theme) => {
  theme.value = newTheme
}

const toggleTheme = () => {
  theme.value = theme.value === 'light' ? 'dark' : 'light'
}

onMounted(() => {
  const savedTheme = localStorage.getItem('theme') as Theme | null
  const initialTheme = savedTheme || 'light' // Default to light theme

  theme.value = initialTheme
  isInitialized.value = true
})

watch([theme, isInitialized], ([newTheme, newIsInitialized]) => {
  if (newIsInitialized) {
    localStorage.setItem('theme', newTheme)

    const shouldBeDark = newTheme === 'system'
      ? window.matchMedia('(prefers-color-scheme: dark)').matches
      : newTheme === 'dark'

    if (shouldBeDark) {
      document.documentElement.classList.add('dark')
    } else {
      document.documentElement.classList.remove('dark')
    }
  }
})

provide<ThemeContext>('theme', {
  isDarkMode,
  toggleTheme,
  setTheme,
  currentTheme,
})
</script>

<script lang="ts">
import { inject, type ComputedRef } from 'vue'

export type Theme = 'light' | 'dark' | 'system'

export interface ThemeContext {
  isDarkMode: ComputedRef<boolean>
  toggleTheme: () => void
  setTheme: (theme: Theme) => void
  currentTheme: ComputedRef<Theme>
}

export function useTheme() {
  const theme = inject<ThemeContext>('theme')
  if (!theme) {
    throw new Error('useTheme must be used within a ThemeProvider')
  }
  return theme
}
</script>
