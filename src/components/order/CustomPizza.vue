<template>
  <div class="custom-pizza">
    <h3 class="custom-pizza__title">Custom Pizza</h3>

    <!-- Size Selection -->
    <div class="size-selection">
      <h4 class="size-selection__title">Size</h4>
      <div class="size-selection__options">
        <div v-for="size in sizeList" :key="size.id" class="size-option">
          <input
            type="radio"
            :id="`size-${size.id}`"
            :value="size.id"
            v-model="selectedSizeId"
            class="size-option__radio"
            @change="$emit('size-change', size.id)"
          />
          <label :for="`size-${size.id}`" class="size-option__label">
            {{ size.name }}
            <span v-if="size.extra_price > 0" class="size-option__price">
              (+{{ size.extra_price }}$)
            </span>
          </label>
        </div>
      </div>
    </div>

    <!-- Toppings Selection -->
    <div class="toppings-selection">
      <h4 class="toppings-selection__title">Toppings</h4>
      <div class="toppings-selection__grid">
        <div
          v-for="topping in toppingList"
          :key="topping.id"
          class="topping-option"
          :class="{ 'topping-option--disabled': !isToppingAllowed(topping.id) }"
        >
          <input
            type="checkbox"
            :id="`topping-${topping.id}`"
            :value="topping.id"
            v-model="selectedToppings"
            :disabled="!isToppingAllowed(topping.id)"
            class="topping-option__checkbox"
            @change="$emit('toppings-change', selectedToppings)"
          />
          <label :for="`topping-${topping.id}`" class="topping-option__label">
            {{ topping.name }}
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, watch } from "vue";

const props = defineProps({
  sizeList: {
    type: Array,
    required: true,
  },
  toppingList: {
    type: Array,
    required: true,
  },
  initialSizeId: {
    type: Number,
    default: 1,
  },
  initialToppings: {
    type: Array,
    default: () => [],
  },
  allowedToppings: {
    type: Array,
    default: () => [],
  },
});

defineEmits(["size-change", "toppings-change"]);

const selectedSizeId = ref(props.initialSizeId);
const selectedToppings = ref(props.initialToppings);

const isToppingAllowed = (toppingId) => {
  return props.allowedToppings.includes(toppingId);
};

watch(
  () => props.initialSizeId,
  (newVal) => {
    selectedSizeId.value = newVal;
  }
);

watch(
  () => props.initialToppings,
  (newVal) => {
    selectedToppings.value = newVal;
  }
);
</script>

<style lang="scss" scoped>
@use "@/assets/scss/order/custom-pizza.scss";
</style>
