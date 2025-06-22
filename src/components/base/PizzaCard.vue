<!-- src/components/PizzaCard.vue -->
<template>
  <div class="pizza-card" :class="{ 'pizza-card--selected': isSelected }">
    <input
      type="radio"
      :id="`pizza-${pizza.id}`"
      :value="pizza.id"
      :checked="isSelected"
      class="pizza-card__radio"
      @change="$emit('select', pizza)"
    />
    <label :for="`pizza-${pizza.id}`" class="pizza-card__label">
      <div class="pizza-card__image">
        <div v-if="!getPizzaImage(pizza.name)" class="pizza-card__placeholder"></div>
        <img v-else :src="getPizzaImage(pizza.name)" :alt="pizza.name" />
      </div>
      <div class="pizza-card__info">
        <h3 class="pizza-card__name">{{ pizza.name }}</h3>
        <div class="pizza-card__price">
          <span class="pizza-card__price--final">
            ${{ pizza.discount.final_price.toFixed(2) }}
          </span>
          <span v-if="pizza.discount.is_active" class="pizza-card__price--original">
            ${{ pizza.price.toFixed(2) }}
          </span>
        </div>
      </div>
      <div v-if="pizza.discount.is_active" class="pizza-card__offer">
        <img :src="ribbon" alt="discount" />
      </div>
    </label>
  </div>
</template>

<script setup>
import ribbon from "/assets/img/ribbon.svg";
defineProps({
  pizza: Object,
  isSelected: Boolean,
});

defineEmits(["select"]);

function getPizzaImage(name) {
  return name ? `/assets/img/pizza/${name}.png` : null;
}
</script>

<style scoped lang="scss">
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;
// Pizza Card
.pizza-card {
  border-radius: 12px;
  border: 1px solid $border-color;
  overflow: hidden;
  @include transition;
  position: relative;
  cursor: pointer;

  &:hover:not(&--selected) {
    background-color: $secondary-color;

    .pizza-card__image > img {
      transform: rotate(15deg);
    }
  }

  &__radio {
    display: none;
  }

  &__label {
    display: flex;
    align-items: center;
    cursor: pointer;
    padding: 1.25rem;
    gap: 1.5rem;
  }

  &__image {
    height: auto;
    min-height: 3rem;
    position: relative;
    overflow: hidden;
    display: flex;
    align-items: center;

    & > img {
      width: 100%;
      height: 7em;
      object-fit: contain;
      transform: rotate(0deg);
      @include transition(transform, 0.3s);
    }
  }

  &__placeholder {
    width: 100%;
    height: 100%;
    background: radial-gradient(circle at center, rgba(255, 255, 255, 0.2) 30%, transparent 30%);
    background-size: 20px 20px;
  }

  &__info {
    position: relative;
  }

  &__name {
    font-size: 1rem;
    font-weight: 700;
    line-height: 1.5;
    margin-bottom: 0.25rem;
  }

  &__price {
    font-size: 1rem;
    line-height: 1.5;
    display: flex;
    align-items: center;
    gap: 10px;

    &--original {
      text-decoration: line-through;
      color: $text-light;
      font-weight: 300;
    }
  }

  &__offer {
    position: absolute;
    top: 0;
    right: 0;

    & > img {
      height: 80px;
    }
  }

  &--selected {
    background-color: $primary-color;

    & .pizza-card__image > img {
      transform: rotate(15deg);
    }

    & .pizza-card__name {
      color: $white;
    }

    & .pizza-card__price {
      &--original {
        color: #efbb8b;
      }
      &--final {
        color: $white;
      }
    }
  }
}
</style>
