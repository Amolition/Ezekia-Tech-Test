<script setup lang="ts">
import { reactive, toRefs, onBeforeMount, type DeepReadonly } from 'vue'
import CardItem from './CardItem.vue'

const pageTitle = 'space'

const props = defineProps<{
  rawData: DeepReadonly<
    {
      [key in `${typeof pageTitle}Highlights`]: {
        date: string
        description: string
        id: number
        image: string
        name: string
        news?: {
          date?: string
          title: string
        }
        quiz?: string
      }[]
    } & {
      [key in `${typeof pageTitle}Partners`]: {
        [key: string]: {
          createdAt: string
          info: string
          image: string
          name: string
        }
      }
    }
  >
}>()

const { rawData } = toRefs(props)

type highlightsAttrs = Exclude<keyof (typeof rawData.value.spaceHighlights)[number], 'id'>
type partnersAttrs = keyof (typeof rawData.value.spacePartners)[string]

const getHighlightValue = (id: number, attribute: highlightsAttrs) => {
  return rawData.value.spaceHighlights.find((x) => x.id === id)?.[attribute]
}
const getPartnerValue = (id: string, attribute: partnersAttrs) => {
  return rawData.value.spacePartners[id][attribute as partnersAttrs]
}

const getValue = (id: number | string, attribute: highlightsAttrs | partnersAttrs) => {
  if (typeof id === 'number') return getHighlightValue(id, attribute as highlightsAttrs)
  else return getPartnerValue(id, attribute as partnersAttrs)
}

let displayOrder: (number | string)[] = reactive([
  ...rawData.value.spaceHighlights.map((obj) => obj.id),
  ...(Object.keys(rawData.value.spacePartners) as (keyof typeof rawData.value.spacePartners)[]),
])
const reorderCards = (method: 'date', direction: 'asc' | 'desc'): (number | string)[] => {
  if (method === 'date') {
    displayOrder.sort((a, b) => {
      const aDate = getValue(a, typeof a === 'number' ? 'date' : 'createdAt')
      const bDate = getValue(b, typeof b === 'number' ? 'date' : 'createdAt')
      if (typeof aDate !== 'string' || typeof bDate !== 'string') throw Error('invalid date format')
      if (Date.parse(aDate) > Date.parse(bDate)) return direction === 'asc' ? 1 : -1
      else if (Date.parse(aDate) < Date.parse(bDate)) return direction === 'asc' ? -1 : 1
      else return 0
    })
    console.log(displayOrder)
  }
  return displayOrder
}

onBeforeMount(() => {
  reorderCards('date', 'asc')
})
</script>

<template>
  <ol class="card-list">
    <CardItem v-for="id in displayOrder" :key="id">
      <template #image>
        <img class="standard-image" :src="getValue(id, 'image') as (string | undefined)" />
      </template>
      <template #heading>
        {{ getValue(id, 'name') }}
      </template>
      <template #details>
        {{ getValue(id, typeof id === 'number' ? 'description' : 'info') }}
      </template>
    </CardItem>
  </ol>
</template>

<style scoped>
.card-list {
  list-style-type: none;
  display: flex;
  flex-flow: row wrap;
  gap: 40px;
}
</style>
