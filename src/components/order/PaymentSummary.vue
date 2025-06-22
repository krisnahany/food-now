<template>
  <aside class="payment-summary">
    <h3 class="payment-summary__title">Payment Summary</h3>

    <ul class="payment-summary__content">
      <!-- Selected Pizza -->
      <li v-if="selectedPizza" class="payment-item">
        <span class="payment-item__name">{{ selectedPizza.name }}</span>
        <span class="payment-item__price"> {{ selectedPizza.discount.final_price }}$ </span>
      </li>

      <!-- Size -->
      <li v-if="selectedSize" class="payment-item">
        <span class="payment-item__name">Size - {{ selectedSize.name }}</span>
        <span class="payment-item__price"> {{ selectedSize.extra_price }}$ </span>
      </li>

      <!-- Selected Toppings -->
      <li v-for="topping in selectedToppings" :key="topping.id" class="payment-item">
        <span class="payment-item__name">{{ topping.name }}</span>
        <span class="payment-item__price">{{ topping.price }}$</span>
      </li>
    </ul>

    <!-- Total -->
    <div class="payment-summary__total">
      <span class="payment-summary__total-label">Total Price</span>
      <span class="payment-summary__total-price">${{ totalPrice.toFixed(2) }}</span>
    </div>

    <!-- Order Button -->
    <button
      class="payment-summary__order-btn"
      :disabled="!selectedPizza"
      @click="$emit('order', orderData)"
    >
      Order Now
    </button>
  </aside>
</template>

<script setup>
import { computed } from "vue";

const props = defineProps({
  selectedPizza: {
    type: Object,
    default: null,
  },
  selectedSize: {
    type: Object,
    default: null,
  },
  selectedToppings: {
    type: Array,
    default: () => [],
  },
});

const totalPrice = computed(() => {
  let total = 0;

  // Add pizza price
  if (props.selectedPizza) {
    total += props.selectedPizza.discount.final_price;
  }

  // Add size extra price
  if (props.selectedSize) {
    total += props.selectedSize.extra_price;
  }

  // Add toppings price
  total += props.selectedToppings.reduce((sum, topping) => sum + topping.price, 0);

  return total;
});

const orderData = computed(() => ({
  pizza: props.selectedPizza,
  size: props.selectedSize,
  toppings: props.selectedToppings,
  total: totalPrice.value,
}));

defineEmits(["order"]);
</script>

<style lang="scss" scoped>
@use "@/assets/scss/order/payment-summary.scss";
</style>
