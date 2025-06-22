<template>
  <section class="pizza-order__hero">
    <img
      src="/assets/img/hero.png"
      alt="hero"
      class="pizza-order__hero-image"
      fetchpriority="high"
    />
    <h1 class="pizza-order__hero-title">Pizza order</h1>
  </section>
</template>

<style lang="scss" scoped>
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

.pizza-order__hero {
  position: relative;
  height: 80vh;
  display: flex;
  justify-content: center;
  align-items: center;

  &-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: center;
  }

  &-title {
    position: absolute;
    z-index: 1;
    font-size: 4.5rem;
    color: $primary-color;
    font-weight: 700;
  }

  @include responsive(mobile) {
    height: 60vh;
    &-title {
      font-size: 2.5rem;
    }
  }
}
</style>
