<template>
  <div class="flex items-center">
    <ProfileAvatar v-if="showProfileInfo" :address="account" :size="48" />
    <Avatar v-else :size="48" :value="account" />
    <slot :label="label">
      <div class="identity-container">
        <div class="text-k-grey text-base">
          {{ label }}
        </div>
        <component
          :is="disableIdentityLink ? 'div' : NuxtLink"
          class="identity-name font-bold"
          :to="`/${prefix}/u/${account}`">
          <Identity
            :address="account"
            :hide-identity-popover="hideIdentityPopover" />
        </component>
      </div>
    </slot>
  </div>
</template>

<script lang="ts" setup>
import Avatar from '@/components/shared/Avatar.vue'
import Identity from '@/components/identity/IdentityIndex.vue'
import { resolveComponent } from 'vue'

const NuxtLink = resolveComponent('NuxtLink')

withDefaults(
  defineProps<{
    label: string
    account: string
    prefix: string
    hideIdentityPopover?: boolean
    disableIdentityLink?: boolean
    showProfileInfo?: boolean
  }>(),
  {
    hideIdentityPopover: false,
    disableIdentityLink: false,
    showProfileInfo: false,
  },
)
</script>

<style lang="scss" scoped>
.identity {
  &-container {
    padding: 0.625rem;
  }
}
</style>
