<script setup lang="ts">
import { onMounted, ref } from 'vue'

type LinkItem = {
  label: string
  href: string
  icon: string
}

const links: LinkItem[] = [
  { label: 'Portfolio', href: 'https://yourportfolio.com', icon: '↗' },
  { label: 'Instagram', href: 'https://instagram.com', icon: '◌' },
  { label: 'LinkedIn', href: 'https://linkedin.com', icon: 'in' },
  { label: 'Email', href: 'mailto:hello@example.com', icon: '✉' },
]

const isDark = ref(true)

onMounted(() => {
  const savedTheme = window.localStorage.getItem('link-bio-theme')

  if (savedTheme === 'light') {
    isDark.value = false
  } else if (savedTheme === 'dark') {
    isDark.value = true
  }
})

function toggleTheme() {
  isDark.value = !isDark.value
  window.localStorage.setItem('link-bio-theme', isDark.value ? 'dark' : 'light')
}
</script>

<template>
  <section class="page" :class="{ 'light-theme': !isDark }">
    <div class="card">
      <button class="theme-toggle" type="button" @click="toggleTheme" :aria-pressed="isDark ? 'true' : 'false'">
        <span class="toggle-icon" aria-hidden="true">{{ isDark ? '☀' : '☾' }}</span>
        <span>{{ isDark ? 'Light mode' : 'Dark mode' }}</span>
      </button>

      <div class="avatar" aria-label="Profile photo placeholder">
        <div class="avatar-ring">
          <span>Photo</span>
        </div>
      </div>

      <div class="intro">
        <h1>Alicia Kim</h1>
        <p class="tagline">Designer, developer, and storyteller creating calm, human-centered digital experiences.</p>
      </div>

      <nav class="links" aria-label="Quick links">
        <a
          v-for="link in links"
          :key="link.label"
          class="link-button"
          :href="link.href"
          target="_blank"
          rel="noopener noreferrer"
        >
          <span class="link-icon" aria-hidden="true">{{ link.icon }}</span>
          <span>{{ link.label }}</span>
        </a>
      </nav>
    </div>
  </section>
</template>

<style scoped>
.page {
  min-height: 100vh;
  display: grid;
  place-items: center;
  padding: 1.25rem;
  background: radial-gradient(circle at top, #243b53 0%, #0d1426 45%, #060816 100%);
  color: #edf2ff;
  transition: background 0.3s ease, color 0.3s ease;
}

.page.light-theme {
  background: linear-gradient(135deg, #f6f8ff 0%, #e9eefc 100%);
  color: #172033;
}

.card {
  width: min(100%, 480px);
  max-width: 480px;
  padding: 2rem 1.5rem;
  border-radius: 24px;
  border: 1px solid rgba(255, 255, 255, 0.12);
  background: rgba(8, 15, 30, 0.82);
  box-shadow: 0 18px 45px rgba(0, 0, 0, 0.28);
  backdrop-filter: blur(18px);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.25rem;
  transition: background 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}

.light-theme .card {
  background: rgba(255, 255, 255, 0.92);
  border-color: rgba(15, 23, 42, 0.08);
  box-shadow: 0 18px 45px rgba(15, 23, 42, 0.1);
}

.theme-toggle {
  align-self: flex-end;
  display: inline-flex;
  align-items: center;
  gap: 0.45rem;
  border: 0;
  border-radius: 999px;
  padding: 0.5rem 0.8rem;
  background: rgba(255, 255, 255, 0.1);
  color: inherit;
  cursor: pointer;
  transition: transform 0.2s ease, background 0.2s ease;
}

.theme-toggle:hover {
  transform: translateY(-1px);
  background: rgba(255, 255, 255, 0.16);
}

.light-theme .theme-toggle {
  background: rgba(15, 23, 42, 0.06);
}

.light-theme .theme-toggle:hover {
  background: rgba(15, 23, 42, 0.1);
}

.avatar {
  width: 118px;
  height: 118px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  padding: 0.25rem;
  background: linear-gradient(135deg, #6f7dff 0%, #8f5bff 100%);
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2);
}

.avatar-ring {
  width: 100%;
  height: 100%;
  border-radius: 50%;
  border: 2px dashed rgba(255, 255, 255, 0.75);
  display: grid;
  place-items: center;
  color: white;
  font-size: 0.95rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

.intro {
  text-align: center;
}

h1 {
  margin: 0 0 0.35rem;
  font-size: clamp(1.7rem, 4vw, 2.2rem);
}

.tagline {
  margin: 0;
  font-size: 1rem;
  line-height: 1.7;
  opacity: 0.84;
}

.links {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  margin-top: 0.25rem;
}

.link-button {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.65rem;
  width: 100%;
  border-radius: 999px;
  padding: 0.9rem 1rem;
  background: rgba(255, 255, 255, 0.08);
  color: inherit;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: transform 0.2s ease, background 0.2s ease, border-color 0.2s ease;
}

.link-button:hover {
  transform: translateY(-2px);
  background: rgba(255, 255, 255, 0.16);
  border-color: rgba(255, 255, 255, 0.2);
}

.light-theme .link-button {
  background: rgba(15, 23, 42, 0.05);
  border-color: rgba(15, 23, 42, 0.08);
}

.light-theme .link-button:hover {
  background: rgba(15, 23, 42, 0.08);
  border-color: rgba(15, 23, 42, 0.12);
}

.link-icon {
  display: inline-grid;
  place-items: center;
  width: 1.3rem;
  font-weight: 700;
}

@media (min-width: 640px) {
  .card {
    padding: 2.4rem;
  }
}
</style>
