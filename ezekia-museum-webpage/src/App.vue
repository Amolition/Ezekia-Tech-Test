<script setup lang="ts">
import TheHeader from './components/TheHeader.vue'
import TheBody from './components/TheBody.vue'
</script>

<template>
  <header>
    <TheHeader />
  </header>

  <main>
    <TheBody />
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
header {
  height: 100px;
  line-height: 1.5;

  flex: 0 0 auto;
}

main {
  flex: 1 0 auto;
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
