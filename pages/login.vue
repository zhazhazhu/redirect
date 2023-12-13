<script lang='ts' setup>
import { Icon } from '@iconify/vue'
import { githubLoginUri } from '~/constants'

const { public: { state, scope, client_id, client_secret, redirect_uri } } = useRuntimeConfig()

const uri = `${githubLoginUri}?${new URLSearchParams({
  state,
  scope,
  client_id,
  client_secret,
  redirect_uri,
}).toString()}`

onMounted(() => {
  location.href = uri
})
</script>

<template>
  <div>
    <div class="items" b-b="1px solid gray-7">
      <!-- <Icon icon="fluent-emoji:carrot" class="text-4rem" /> -->
      <div class="text-3rem font-bold">
        Picx
      </div>
    </div>
    <div class="items flex-col">
      <div class="text-2rem font-500">
        正在连接 GITHUB
      </div>
      <Icon icon="eos-icons:three-dots-loading" class="text-4rem" />
      <div class="mt-10px flex items-center">
        <Icon icon="gravity-ui:circle-check" class="mr-6px text-1.4rem color-green" />
        <div class="text-.9rem">
          Spotify for Desktop
        </div>
      </div>
    </div>
  </div>
</template>
