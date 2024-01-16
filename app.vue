<script setup lang="ts">
import { appName } from '~/constants'

const route = useRoute()
const colorMode = useColorMode()
const runtimeConfig = useRuntimeConfig()
const redirect = computed(() => runtimeConfig.public.base + route.fullPath)

const isDark = computed({
  get() {
    return colorMode.value === 'dark'
  },
  set() {
    colorMode.preference = colorMode.value === 'dark' ? 'light' : 'dark'
  },
})

useHead({
  title: appName,
})

onMounted(() => {
  setTimeout(() => {
    location.href = redirect.value
  }, 500)
})
</script>

<template>
  <UContainer>
    <div class="flex py-4">
      <div flex-1 />
      <div class="float-end">
        <ClientOnly>
          <UButton
            :icon="isDark ? 'i-heroicons-moon-20-solid' : 'i-heroicons-sun-20-solid'"
            color="gray"
            variant="ghost"
            aria-label="Theme"
            @click="isDark = !isDark"
          />

          <template #fallback>
            <div class="h-8 w-8" />
          </template>
        </ClientOnly>
      </div>
    </div>

    <div class="flex flex-col items-center py-10 text-2xl tracking-wider">
      <div i-line-md-loading-twotone-loop class="h-14 w-14" />
      <div class="py-10">
        Redirecting to {{ runtimeConfig.public.base }}
      </div>
    </div>
  </UContainer>
</template>

<style>
body {
  background-color: #fff;
  color: rgba(0,0,0,0.8);
}
.dark body {
  background-color: #091a28;
  color: #ebf4f1;
}
</style>
