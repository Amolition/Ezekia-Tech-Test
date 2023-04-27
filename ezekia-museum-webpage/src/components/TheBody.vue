<script setup lang="ts">
import { reactive, toRefs, onBeforeMount, type DeepReadonly } from 'vue'
import CardItem from './CardItem.vue'

let pageTitle = 'space'

type newsType = DeepReadonly<{
  date?: string
  title: string
}>

type rawDataType = DeepReadonly<
  {
    [key in `${typeof pageTitle}Highlights`]: {
      date: string
      description: string
      id: number
      image: string
      name: string
      news?: newsType
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

const props = defineProps<{
  rawData: rawDataType
}>()

const { rawData } = toRefs(props)

let icon: { type: string; content: string } | undefined

switch (pageTitle) {
  case 'space':
    icon = {
      type: 'fa',
      content: 'star',
    }
    break
  case 'dinosaurs':
    // not implemented
    break
  case 'wildlife':
    //not implemented
    break
}

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
      <template #icon>
        <font-awesome-icon
          v-if="icon?.type === 'fa'"
          :icon="['fas', icon.content]"
        ></font-awesome-icon>
      </template>
      <template #details>
        <div class="card__description">
          {{ getValue(id, typeof id === 'number' ? 'description' : 'info') }}
        </div>
        <div class="card__news" v-if="getValue(id, 'news')">
          {{ (getValue(id, 'news') as newsType | undefined)?.title }}
          <span class="card__news-lozenge"> news </span>
        </div>
        <div class="card__quiz" v-if="getValue(id, 'quiz')">
          {{ getValue(id, 'quiz') }}
          <span class="card__quiz-lozenge"> quiz </span>
        </div>
      </template>
    </CardItem>
  </ol>
</template>

<style lang="scss" scoped>
.card-list {
  list-style-type: none;
  display: flex;
  flex-flow: row wrap;
  gap: 40px;
}
.card {
  &__news,
  &__quiz {
    margin-top: 10px;
    padding: 10px 0;
  }
  &__news {
    border-top: var(--c-text) 2px solid;
    color: var(--c-red-light);
  }
  &__quiz {
    border-top: var(--c-text) 2px solid;
    color: var(--c-blue-light);
  }
  &__news-lozenge,
  &__quiz-lozenge {
    height: 10px;
    margin-left: 5px;
    padding: 2px 5px;
    font-size: 0.6rem;
    font-weight: bold;
    border-radius: 7px;
    position: relative;
    bottom: 2px;
  }
  &__news-lozenge {
    color: var(--c-red-dark);
    background-color: var(--c-red-light);
  }
  &__quiz-lozenge {
    color: var(--c-blue-dark);
    background-color: var(--c-blue-light);
  }
}
</style>
