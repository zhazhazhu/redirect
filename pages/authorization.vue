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
  <div>
    <div class="items" b-b="1px solid gray-7">
      <div class="text-3rem font-bold">
        Picx
      </div>
    </div>

    <div class="items flex-col">
      <div v-if="code" class="flex items-center color-green">
        <Icon icon="gravity-ui:circle-check" class="my-10px mr-6px text-3rem" />
        <div class="text-2rem font-500">
          GITHUB 授权身份验证成功
        </div>
      </div>
      <div v-else class="flex items-center color-red">
        <Icon icon="gravity-ui:circle-xmark" class="my-10px mr-6px text-3rem" />
        <div class="text-2rem font-500">
          GITHUB 授权身份验证失败
        </div>
      </div>
      <div class="mt-10px flex items-center">
        <Icon icon="gravity-ui:circle-check" class="mr-6px text-1.4rem color-green" />
        <div class="text-.9rem">
          Spotify for Desktop
        </div>
      </div>
    </div>
  </div>
</template>
