<script lang="ts" setup>
import { Icon } from '@iconify/vue'

const route = useRoute()
const router = useRouter()
const code = route.query.code as string
const setup_action = route.query.setup_action as string

async function auth() {
  if (!code)
    return router.push(`/authorization_error?code_error=true`)

  const token = await $fetch('/api/auth', { params: { code } })
  const uri = new URLSearchParams(token).toString()
  if ('error' in token)
    return router.push(`/authorization_error?${uri}`)
  else
    location.href = `picx://authorization?${uri}`
}

function install() {
  location.href = `picx://installations${location.search}`
}

onMounted(async () => {
  if (setup_action && setup_action === 'install')
    return install()

  auth()
})
</script>

<template>
  <div class="flex flex-col items-center pt-60px">
    <Icon icon="icon-park-solid:success" class="text-5rem text-green-500 dark:text-green-400" />
    <div class="mt-20px text-center">
      <template v-if="code">
        <div class="text-1.5rem color-white">
          GitHub authorization authentication successful
        </div>
        <div class="text-1rem color-gray-4">
          about to open the app
        </div>
      </template>
      <template v-else>
        <div class="text-1.5rem color-gray-6">
          GitHub authorization authentication
        </div>
      </template>
    </div>
  </div>
</template>
