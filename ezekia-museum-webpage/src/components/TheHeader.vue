<template>
  <div class="logo-container">
    <font-awesome-icon class="logo-container__logo" :icon="['fas', 'landmark']" />
  </div>
  <h1>Natural History Museum</h1>
  <div class="divider-line"></div>
</template>

<style lang="scss" scoped>
.logo-container {
  padding: 20px;
  width: 100px;
  height: 100px;

  display: flex;
  align-items: center;
  justify-content: center;
  &__logo {
    height: 50px;
  }
}
.divider-line {
  width: 5px;
  height: 100%;
  background-color: var(--c-bg);
}
</style>
