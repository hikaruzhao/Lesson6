<script setup lang="ts">
defineProps<{
  label: string
  url: string
  icon: string
}>()
</script>

<template>
  <v-btn
    :href="url"
    target="_blank"
    rel="noopener noreferrer"
    block
    size="large"
    rounded="pill"
    variant="tonal"
    class="link-button"
  >
    <template #prepend>
      <v-icon :icon="icon" />
    </template>
    {{ label }}
  </v-btn>
</template>

<style scoped>
.link-button :deep(.v-btn__prepend) {
  margin-right: 4px;
}
</style>
