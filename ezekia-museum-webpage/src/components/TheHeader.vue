<script lang="ts" setup>
defineProps<{
  darkModeSate: boolean
}>()
</script>

<template>
  <div class="logo-container">
    <font-awesome-icon class="logo-container__logo" :icon="['fas', 'landmark']" />
  </div>
  <h1 class="main-title">Natural History Museum</h1>
  <div class="divider-line"></div>
  <h2 class="sub-title">Space</h2>
  <slot name="darkThemeToggle"></slot>
</template>

<style lang="scss" scoped>
.logo-container {
  width: fit-content;
  height: 100px;

  display: flex;
  align-items: center;
  justify-content: center;
  &__logo {
    height: 30px;
  }
}
.main-title {
  font-variant: small-caps;
  font-size: 30px;
}
.sub-title {
  text-transform: uppercase;
  font-family: 'Lucida Console';
  font-size: 25px;
  letter-spacing: 3px;
}
.divider-line {
  width: 5px;
  height: 100%;
  background-color: var(--c-bg);
}
</style>
