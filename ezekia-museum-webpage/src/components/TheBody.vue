<script setup lang="ts">
import { reactive, onBeforeMount } from 'vue'
// import type { Reactive } from 'vue'
import CardItem from './CardItem.vue'

import images from '../assets/images/images'

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
      // info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
      info: 'The Mauna Kea Observatories (MKO) are a number of independent astronomical research facilities and large telescope observatories that are located at the summit of Mauna Kea on the Big Island of Hawaiʻi, United States.',
      image: images.observatory,
      name: 'Mauna Kea Observatories',
    },
  },
} as const

type IDs = (typeof rawData.spaceHighlights)[number]['id'] | keyof typeof rawData.spacePartners
type Attrs =
  | Exclude<keyof (typeof rawData.spaceHighlights)[number], 'id'>
  | keyof (typeof rawData.spacePartners)[keyof typeof rawData.spacePartners]
const getValue = (id: IDs, attribute: Attrs) => {
  let returnVal
  const equivalentAttrs = [
    { highlights: 'date', partners: 'createdAt' },
    { highlights: 'description', partners: 'info' },
  ] as const
  if (typeof id === 'number') {
    const equivalent = equivalentAttrs.find((obj) => obj.partners === attribute)
    if (equivalent) attribute = equivalent.highlights
    returnVal = rawData.spaceHighlights.find((item) => item.id === id)![
      attribute as Exclude<Attrs, (typeof equivalentAttrs)[number]['partners']>
    ]
  } else {
    const equivalent = equivalentAttrs.find((obj) => obj.highlights === attribute)
    if (equivalent) attribute = equivalent.partners
    returnVal =
      rawData.spacePartners[id][
        attribute as Exclude<Attrs, (typeof equivalentAttrs)[number]['highlights']>
      ]
  }
  console.log(attribute)
  console.log(returnVal)
  return returnVal
}

let displayOrder: IDs[] = reactive([
  ...rawData.spaceHighlights.map((obj) => obj.id),
  ...(Object.keys(rawData.spacePartners) as (keyof typeof rawData.spacePartners)[]),
])
const reorderCards = (method: 'date', direction: 'asc' | 'desc'): IDs[] => {
  if (method === 'date') {
    displayOrder.sort((a, b) => {
      const aDate = getValue(a, 'date')
      const bDate = getValue(b, 'date')
      if (typeof b === 'string') console.log(Date.parse(aDate) > Date.parse(bDate))
      if (Date.parse(aDate) > Date.parse(bDate)) return direction === 'asc' ? 1 : -1
      else if (Date.parse(aDate) < Date.parse(bDate)) return direction === 'asc' ? -1 : 1
      else return 0
    })
    console.log(displayOrder)
  }
  return displayOrder
}

onBeforeMount(() => {
  console.log('test')
  reorderCards('date', 'asc')
})
</script>

<template>
  <ol>
    <CardItem v-for="id in displayOrder" :key="id">
      <template #image>
        <img class="standard-image" :src="getValue(id, 'image')" />
      </template>
      <template #heading>{{ getValue(id, 'name') }}</template>
      <template #details>{{ getValue(id, 'description') }}</template>

      Vue’s
      <a href="https://vuejs.org/" target="_blank" rel="noopener">official documentation</a>
      provides you with all information you need to get started.
    </CardItem>
  </ol>

  <!-- 
  <CardItem>
    <template #icon>
      <SupportIcon />
    </template>
    <template #heading>Support Vue</template>

    As an independent project, Vue relies on community backing for its sustainability. You can help
    us by
    <a href="https://vuejs.org/sponsor/" target="_blank" rel="noopener">becoming a sponsor</a>.
  </CardItem>
   -->
</template>
