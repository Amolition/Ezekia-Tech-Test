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
  width: 300px;
  height: 300px;
  overflow: hidden;
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
  }
  &__heading {
    display: flex;
    flex-flow: row;
    align-items: center;
    background: var(--c-bg-card-header);
    opacity: 0.7;

    padding: 0 20px;
    width: 100%;
    height: 50px;
  }
  &__details {
    padding: 0 20px;
  }
}

i {
  display: flex;
  place-items: center;
  place-content: center;
  width: 32px;
  height: 32px;

  color: var(--c-text);
}

h3 {
  font-size: 1.2rem;
  font-weight: 500;
  margin-bottom: 0.4rem;
  color: var(--c-heading);
}

@media (min-width: 1024px) {
  .item {
    margin-top: 0;
    padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
  }

  i {
    top: calc(50% - 25px);
    left: -26px;
    position: absolute;
    border: 1px solid var(--c-border);
    background: var(--c-bg);
    border-radius: 8px;
    width: 50px;
    height: 50px;
  }

  .item:before {
    content: ' ';
    border-left: 1px solid var(--c-border);
    position: absolute;
    left: 0;
    bottom: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:after {
    content: ' ';
    border-left: 1px solid var(--c-border);
    position: absolute;
    left: 0;
    top: calc(50% + 25px);
    height: calc(50% - 25px);
  }

  .item:first-of-type:before {
    display: none;
  }

  .item:last-of-type:after {
    display: none;
  }
}
</style>
