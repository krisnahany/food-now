<template>
  <div class="pizza-list">
    <h2 class="pizza-list__title">Choose your pizza</h2>

    <!-- Pre-made Pizzas -->
    <div class="pizza-list__grid">
      <PizzaCard
        v-for="pizza in pizzaList"
        :key="pizza?.id"
        :pizza="pizza"
        :isSelected="selectedPizzaId === pizza?.id"
        @select="$emit('select', pizza)"
      />
    </div>
  </div>
</template>

<script setup>
import PizzaCard from "@/components/base/PizzaCard.vue";

defineProps({
  pizzaList: {
    type: Array,
    required: true,
  },
  selectedPizzaId: {
    type: Number,
    default: null,
  },
});

defineEmits(["select"]);
</script>

<style lang="scss" scoped>
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

.pizza-list {
  margin-bottom: clamp(50px, 8vw, 100px);

  &__title {
    font-size: clamp(1.5rem, 3vw, 2.25rem);
    font-weight: 700;
    color: $primary-color;
    margin-bottom: clamp(20px, 4vh, 30px);

    @include responsive(mobile) {
      font-size: 1.5rem;
      margin-bottom: 20px;
    }
  }

  &__grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;

    @include responsive(mobile) {
      grid-template-columns: 1fr;
      gap: 15px;
    }
    @include responsive(desktop) {
      grid-template-columns: repeat(2, 1fr);
      gap: 20px;
    }
  }
}
</style>
