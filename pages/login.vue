<script lang='ts' setup>
import { Icon } from '@iconify/vue'

const { public: { state, scope, client_id, client_secret, redirect_uri } } = useRuntimeConfig()

const uri = `https://github.com/login/oauth/authorize?${new URLSearchParams({
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
  <div h-100vh>
    <div class="pt-50px text-center">
      <div class="mb-30px w-full flex flex-col items-center">
        <Icon icon="mdi:github" class="text-8rem" />
        <div
          class="base-text-color my-20px text-2rem font-bold lh-38px text-green-500 dark:text-green-400"
        >
          Login with Github loading...
        </div>
        <p class="my-0 color-gray" />
      </div>
    </div>
  </div>
</template>
