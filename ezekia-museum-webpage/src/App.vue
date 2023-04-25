<script setup lang="ts">
import TheHeader from './components/TheHeader.vue'
import TheBody from './components/TheBody.vue'

import images from './assets/images/images'

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
</script>

<template>
  <header class="header">
    <TheHeader />
  </header>

  <main class="body">
    <TheBody :rawData="rawData" />
  </main>
</template>

<style>
.standard-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
</style>

<style scoped>
.header {
  height: 100px;
  line-height: 1.5;

  flex: 0 0 auto;

  background: var(--c-bg-mute);
  display: flex;
  flex-flow: row;
  gap: 20px;
}

.body {
  flex: 1 0 auto;
  padding: 40px;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
