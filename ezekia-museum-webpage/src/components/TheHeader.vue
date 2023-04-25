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
:slotted(.dark-mode-toggle-container) {
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
