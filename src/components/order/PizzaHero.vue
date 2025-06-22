<template>
  <section class="pizza-order__hero">
    <h1 class="pizza-order__hero-title">Pizza order</h1>
  </section>
</template>

<style lang="scss" scoped>
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

.pizza-order__hero {
  position: relative;
  background: url("/assets/img/hero.png") center/cover no-repeat;
  min-height: 80vh;
  display: flex;
  justify-content: center;
  align-items: center;

  &-title {
    position: absolute;
    z-index: 1;
    font-size: 4.5rem;
    color: $primary-color;
    font-weight: 700;
  }

  @include responsive(mobile) {
    min-height: 100vh;
    &-title {
      font-size: 2.5rem;
    }
  }
}
</style>
