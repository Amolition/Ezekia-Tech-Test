<template>
  <li class="card">
    <div class="card__image">
      <slot name="image"></slot>
    </div>
    <div class="card__info">
      <h3 class="card__heading">
        <span class="card__heading-title">
          <slot name="heading"></slot>
        </span>
        <div class="card__icon">
          <slot name="icon"></slot>
        </div>
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
    transition: filter 0.2s;
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
    justify-content: space-between;
    background: var(--c-bg-card-header);
    opacity: 1;
    font-size: 1.25rem;

    padding: 0 20px;
    width: 100%;
    height: 50px;
  }
  &__heading-title {
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }
  &__details {
    padding: 0 20px;
    padding-top: 10px;
    opacity: 0;
    transition: opacity 0.2s;
  }
  &:hover {
    transform: scale(1.1);
    .card__image {
      filter: brightness(30%);
    }
    .card__details {
      opacity: 1;
    }
  }
}
</style>
