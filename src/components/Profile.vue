<script setup lang="ts">
defineProps<{
  label?: string
  photo?: string
  icon?: string
}>()
</script>

<template>
  <div v-if="photo" class="profile-avatar profile-avatar--image">
    <v-img :src="photo" alt="Profile photo" cover />
  </div>

  <div v-else class="profile-avatar profile-avatar--placeholder" color="primary">
    <template v-if="icon">
      <v-icon :icon="icon" size="32" />
    </template>
    <span v-else-if="label" class="text-h6 font-weight-bold">{{ label }}</span>
  </div>
</template>

<style scoped>
.profile-avatar {
  width: 200px;
  height: 200px;
  border: 0px solid rgba(255, 255, 255, 0.2);
  overflow: hidden;
  position: relative;
  margin: 0 auto;
  background-color: rgb(var(--v-theme-primary));
  clip-path: polygon(30% 0%, 70% 0%, 100% 30%, 100% 70%, 70% 100%, 30% 100%, 0% 70%, 0% 30%);
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
}

.profile-avatar--image {
  background-color: transparent;
}

.profile-avatar--placeholder {
  color: white;
}
</style>
