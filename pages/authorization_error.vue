<script lang='ts' setup>
import { Icon } from '@iconify/vue'

const route = useRoute()
const code_error = Boolean(route.query.code_error)
const error = route.query.error as string
const error_description = route.query.error_description as string
const error_uri = route.query.error_uri as string
</script>

<template>
  <div class="flex flex-col items-center pt-60px">
    <Icon icon="bxs:error" class="text-8rem color-red" />
    <template v-if="code_error">
      <div>
        error: code is undefine
      </div>
    </template>
    <template v-else>
      <div v-if="error">
        error: {{ error }}
      </div>
      <div v-if="error_description">
        error_description: {{ error_description }}
      </div>
      <ULink
        :to="error_uri"
        active-class="text-primary"
        inactive-class="text-green-500 dark:text-green-400 hover:text-green-700 dark:hover:text-green-200"
      >
        Click to view errors docs
      </ULink>
    </template>
  </div>
</template>
