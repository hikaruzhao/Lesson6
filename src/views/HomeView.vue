<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useTheme } from 'vuetify'
import LinkButton from '@/components/LinkButton.vue'

type LinkItem = {
  label: string
  href: string
  icon: string
}

const links: LinkItem[] = [
  { label: 'Portfolio', href: 'https://yourportfolio.com', icon: 'mdi-open-in-new' },
  { label: 'Instagram', href: 'https://instagram.com', icon: 'mdi-instagram' },
  { label: 'LinkedIn', href: 'https://linkedin.com', icon: 'mdi-linkedin' },
  { label: 'Email', href: 'mailto:hello@example.com', icon: 'mdi-email' },
]

const theme = useTheme()
const isDark = ref(theme.global.current.value.dark)

onMounted(() => {
  const savedTheme = window.localStorage.getItem('link-bio-theme')

  if (savedTheme === 'light') {
    theme.global.name.value = 'light'
    isDark.value = false
  } else if (savedTheme === 'dark') {
    theme.global.name.value = 'dark'
    isDark.value = true
  }
})

function toggleTheme() {
  const nextDark = !isDark.value
  isDark.value = nextDark
  theme.global.name.value = nextDark ? 'dark' : 'light'
  window.localStorage.setItem('link-bio-theme', nextDark ? 'dark' : 'light')
}
</script>

<template>
  <v-container fluid class="fill-height pa-0 page-shell">
    <v-row class="fill-height ma-0" justify="center" align="center">
      <v-col cols="12" sm="8" md="6" lg="4" class="d-flex justify-center">
        <v-card class="pa-6 pa-sm-8 rounded-xl elevation-8 w-100" style="max-width: 480px;">
          <div class="d-flex justify-end" style="margin-bottom: 4px;">
            <v-btn
              :icon="isDark ? 'mdi-weather-sunny' : 'mdi-weather-night'"
              variant="text"
              rounded="pill"
              color="primary"
              @click="toggleTheme"
              :aria-label="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
            />
          </div>

          <div class="d-flex flex-column align-center text-center" style="gap: 4px;">
            <v-avatar size="120" color="primary" rounded="circle">
              <span class="text-h6 font-weight-bold">Photo</span>
            </v-avatar>

            <h1 class="text-h4 font-weight-bold">Hikaru Zhao</h1>
            <p class="text-body-1 text-medium-emphasis" style="padding-bottom: 16px;">
              Designer, developer, and storyteller creating calm, human-centered digital experiences.
            </p>

            <div class="w-100" style="margin-top: 4px; display: flex; flex-direction: column; gap: 8px;">
              <LinkButton
                v-for="link in links"
                :key="link.label"
                :label="link.label"
                :url="link.href"
                :icon="link.icon"
              />
            </div>
          </div>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<style scoped>
.page-shell {
  min-height: 100dvh;
  background: linear-gradient(135deg, #162b4d 0%, #0b172b 48%, #071120 100%);
}
</style>
