<template>
  <li class="card">
    <div class="card__image">
      <slot name="image"></slot>
    </div>
    <div class="card__info">
      <h3 class="card__heading">
        <slot name="heading"></slot>
      </h3>
      <p class="card__details">
        <slot name="details"></slot>
      </p>
    </div>
  </li>
</template>

<style lang="scss" scoped>
.card {
  border-radius: 20px;
  border: solid 3px var(--c-border);
  width: 300px;
  height: 300px;
  overflow: hidden;
  color: var(--c-text);
  transition: transform 0.2s;
  cursor: pointer;
  &__image {
    overflow: hidden;
    position: absolute;
    width: 100%;
    height: 100%;
  }
  &__info {
    display: flex;
    flex-flow: column;
    flex: 1;
    position: absolute;
    width: 100%;
  }
  &__heading {
    display: flex;
    flex-flow: row;
    align-items: center;
    background: var(--c-bg-card-header);
    opacity: 1;
    font-size: 1.25rem;

    padding: 0 20px;
    width: 100%;
    height: 50px;
  }
  &__details {
    padding: 0 20px;
  }
  &:hover {
    transform: scale(1.1);
  }
}
</style>
