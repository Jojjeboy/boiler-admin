<template>
  <AdminLayout>
    <PageBreadcrumb :pageTitle="currentPageTitle" />
    <div class="min-h-screen rounded-2xl border border-gray-200 bg-white px-5 py-7 dark:border-gray-800 dark:bg-white/[0.03] xl:px-10 xl:py-12">
      <div class="mx-auto w-full max-w-[630px]">
        <h3 class="mb-6 font-semibold text-gray-800 text-theme-xl dark:text-white/90 sm:text-2xl">
          {{ $t('common.settings') }}
        </h3>

        <div class="space-y-8">
           <!-- Language Settings -->
           <div class="flex flex-col gap-4 p-5 rounded-xl border border-gray-200 dark:border-gray-800">
             <span class="font-medium text-gray-800 dark:text-white/90">{{ $t('common.language') }}</span>
             <div class="grid grid-cols-2 gap-3">
               <button
                 v-for="lang in languages"
                 :key="lang.value"
                 @click="setLocale(lang.value)"
                 :class="[
                   'px-4 py-2 text-sm rounded-lg border transition-colors',
                   currentLocale === lang.value
                     ? 'bg-brand-50 border-brand-500 text-brand-600 dark:bg-brand-500/10 dark:border-brand-500 dark:text-brand-400'
                     : 'bg-white border-gray-300 text-gray-600 dark:bg-gray-900 dark:border-gray-700 dark:text-gray-400'
                 ]"
               >
                 {{ lang.label }}
               </button>
             </div>
           </div>

          <!-- Theme Settings -->
          <div class="flex flex-col gap-4 p-5 rounded-xl border border-gray-200 dark:border-gray-800">
            <span class="font-medium text-gray-800 dark:text-white/90">{{ $t('common.theme') }}</span>
            <div class="grid grid-cols-3 gap-3">
              <button
                v-for="mode in themeModes"
                :key="mode"
                @click="setTheme(mode)"
                :class="[
                  'px-4 py-2 text-sm rounded-lg border transition-colors',
                  currentTheme === mode
                    ? 'bg-brand-50 border-brand-500 text-brand-600 dark:bg-brand-500/10 dark:border-brand-500 dark:text-brand-400'
                    : 'bg-white border-gray-300 text-gray-600 dark:bg-gray-900 dark:border-gray-700 dark:text-gray-400'
                ]"
              >
                {{ $t(`common.${mode}`) }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </AdminLayout>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import { useI18n } from 'vue-i18n';
import { useTheme, type Theme } from '@/components/layout/ThemeProvider.vue';
import AdminLayout from '@/components/layout/AdminLayout.vue';
import PageBreadcrumb from '@/components/common/PageBreadcrumb.vue';
import i18n from '@/i18n';

const { locale } = useI18n();
const { setTheme, currentTheme } = useTheme();

const currentPageTitle = computed(() => i18n.global.t('common.settings'));
const currentLocale = ref(locale.value);
const languages = [
  { value: 'sv', label: 'Svenska' },
  { value: 'en', label: 'English' },
];
const themeModes: Theme[] = ['light', 'dark', 'system'];

const setLocale = (lang: string) => {
  currentLocale.value = lang;
  locale.value = lang;
  localStorage.setItem('locale', lang);
};
</script>
