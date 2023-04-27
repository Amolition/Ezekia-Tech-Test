<script setup lang="ts">
import { ref, watchEffect } from 'vue'
import TheHeader from './components/TheHeader.vue'
import TheBody from './components/TheBody.vue'
import images from './assets/images/images'

// data that could be received from server
const rawData = {
  spaceHighlights: [
    {
      date: '2020-04-20 12:20:00',
      description:
        'Asteroids are minor planets, especially of the inner Solar System. Larger asteroids have also been called planetoids.',
      id: 1,
      image: images.asteroid,
      name: 'Asteroids',
    },
    {
      date: '2020-05-20 15:50:00',
      description:
        'A comet is an icy, small Solar System body that, when passing close to the Sun, warms and begins to release gases, a process called outgassing.',
      id: 9,
      image: images.comet,
      name: 'Comets',
    },
    {
      date: '2020-05-01 9:22:00',
      description:
        'The term planet is ancient, with ties to history, astrology, science, mythology, and religion.',
      id: 7,
      image: images.planet,
      name: 'Planets',
      news: {
        date: '2020-08-18 18:00:00',
        title: 'Attend our talk about Jupiter with Dr. Hogarth',
      },
      quiz: 'https://planetquiz.space',
    },
    {
      date: '2020-07-05 4:10:00',
      description:
        'A meteor shower is a celestial event in which a number of meteors are observed to radiate, or originate, from one point in the night sky.',
      id: 12,
      image: images.meteors,
      name: 'Meteor showers',
      news: {
        title: 'The Lyrids will peak at on April 21-22 2021, at night',
      },
    },
  ],
  spacePartners: {
    observatory: {
      createdAt: '2020-06-01 11:45:00',
      info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
      image: images.observatory,
      name: 'Mauna Kea Observatories',
    },
  },
} as const

// dark mode logic
const isClientDarkMode = () => {
  return window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches
}
const setDarkTheme = (bool: boolean) => {
  if (bool) document.body.classList.add('dark-mode')
  else document.body.classList.remove('dark-mode')
}
const darkThemeState = ref(isClientDarkMode())
watchEffect(() => setDarkTheme(darkThemeState.value))
</script>

<template>
  <header class="header" @toggle-dark-mode="setDarkTheme">
    <TheHeader :dark-mode-sate="true">
      <template #darkThemeToggle>
        <div class="dark-mode-toggle-container">
          <font-awesome-icon class="dark-mode-toggle__off-icon" :icon="['fas', 'sun']" />
          <button
            class="dark-mode-toggle"
            :class="darkThemeState ? 'dark-mode-toggle--on' : 'dark-mode-toggle--off'"
            @click="darkThemeState = !darkThemeState"
          >
            <span class="dark-mode-toggle__slider"></span>
          </button>
          <font-awesome-icon class="dark-mode-toggle__on-icon" :icon="['fas', 'moon']" />
        </div>
      </template>
    </TheHeader>
  </header>
  <main class="body">
    <TheBody :raw-data="rawData" />
  </main>
</template>

<style>
.standard-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>

<style lang="scss" scoped>
.header {
  height: 100px;
  line-height: 100px;
  flex: 0 0 auto;
  background: var(--c-bg-mute);
  color: var(--c-heading);
  display: flex;
  flex-flow: row;
  gap: 30px;
  padding: 0 30px;
}
.body {
  flex: 1 0 auto;
  padding: 40px;
}
.dark-mode-toggle-container {
  margin: auto 0;
  margin-left: auto;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
  .dark-mode-toggle {
    position: relative;
    display: inline-block;
    width: 60px;
    height: 34px;
    border: none;
    background: none;
    &__slider {
      position: absolute;
      cursor: pointer;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      background-color: #ccc;
      -webkit-transition: 0.4s;
      transition: 0.4s;
      border-radius: 34px;
      &:before {
        position: absolute;
        content: '';
        height: 26px;
        width: 26px;
        left: 4px;
        bottom: 4px;
        background-color: white;
        -webkit-transition: 0.4s;
        transition: 0.4s;
        border-radius: 50%;
      }
    }
    &__on-icon,
    &__off-icon {
      width: 20px;
      height: 20px;
    }
    &--off {
      .dark-mode-toggle__slider {
        background-color: var(--c-green-dark);
      }
    }
    &--on {
      .dark-mode-toggle__slider {
        background-color: var(--c-green-light);
        &:before {
          -webkit-transform: translateX(26px);
          -ms-transform: translateX(26px);
          transform: translateX(26px);
        }
      }
    }
  }
}
</style>
