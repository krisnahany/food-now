<template>
  <div class="pizza-order">
    <!-- Hero Section -->
    <PizzaHero />

    <!-- Content Section -->
    <section class="pizza-order__main">
      <div class="pizza-order__container">
        <div>
          <!-- Pizza List Section -->
          <PizzaList
            :pizza-list="pizzaList"
            :selected-pizza-id="selectedPizzaId"
            @select="handlePizzaSelection"
          />

          <!-- Custom Pizza Section -->
          <CustomPizza
            :size-list="sizeList"
            :topping-list="toppingList"
            :initial-size-id="selectedSizeId"
            :initial-toppings="selectedToppings"
            :allowed-toppings="selectedPizza?.toppings || []"
            @size-change="handleSizeSelection"
            @toppings-change="handleToppingSelection"
          />
        </div>

        <!-- Payment Summary -->
        <PaymentSummary
          :selected-pizza="selectedPizza"
          :selected-size="selectedSize"
          :selected-toppings="selectedToppingsData"
          @order="handleOrder"
        />
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";
import PizzaHero from "@/components/order/PizzaHero.vue";
import PizzaList from "@/components/order/PizzaList.vue";
import CustomPizza from "@/components/order/CustomPizza.vue";
import PaymentSummary from "@/components/order/PaymentSummary.vue";

// Reactive data
const pizzaList = ref([]);
const sizeList = ref([]);
const toppingList = ref([]);
const selectedPizzaId = ref(null);
const selectedSizeId = ref(null);
const selectedToppings = ref([]);

// Computed properties
const selectedPizza = computed(() =>
  pizzaList.value.find((pizza) => pizza.id === selectedPizzaId.value)
);

const selectedSize = computed(() =>
  sizeList.value.find((size) => size.id === selectedSizeId.value)
);

const selectedToppingsData = computed(() =>
  toppingList.value.filter((topping) => selectedToppings.value.includes(topping.id))
);

// Methods
const fetchData = async () => {
  try {
    const pizzaRes = await fetch("/assets/json/pizza-list.json");
    const pizzaData = await pizzaRes.clone().json();
    pizzaList.value = pizzaData.data;

    const sizeRes = await fetch("/assets/json/size-list.json");
    const sizeData = await sizeRes.clone().json();
    sizeList.value = sizeData.data;

    const toppingRes = await fetch("/assets/json/topping-list.json");
    const toppingData = await toppingRes.clone().json();
    toppingList.value = toppingData.data;
  } catch (error) {
    console.error("Error loading data:", error);
  }
};

const handlePizzaSelection = (pizza) => {
  selectedPizzaId.value = pizza.id;

  // Reset size to Small when pizza changes
  selectedSizeId.value = 1;

  // Clear and update toppings based on new pizza
  updateToppingsForPizza();
};

const handleSizeSelection = (sizeId) => {
  selectedSizeId.value = sizeId;
};

const handleToppingSelection = (toppings) => {
  selectedToppings.value = toppings;
};

const updateToppingsForPizza = () => {
  if (!selectedPizza.value) {
    selectedToppings.value = [];
    return;
  }

  // Remove any toppings that are not allowed for the new pizza
  selectedToppings.value = selectedToppings.value.filter((toppingId) =>
    selectedPizza.value.toppings.includes(toppingId)
  );
};

const handleOrder = (orderData) => {
  if (!selectedPizza.value) {
    alert("Please select a pizza first!");
    return;
  }
  console.log("Order placed:", orderData);
  alert(`Order placed! Total: $${orderData.total.toFixed(2)}`);
};

// Lifecycle
onMounted(fetchData);
</script>

<style lang="scss">
@use "@/assets/scss/variables.scss" as *;
@use "@/assets/scss/mixins.scss" as *;

.pizza-order {
  min-height: 100vh;
  display: flex;
  flex-direction: column;

  &__main {
    padding: 100px 0;
  }

  &__container {
    display: grid;
    grid-template-columns: 1fr 300px;
    gap: 25px;
    & {
      @include container;
    }

    @include responsive(tablet) {
      grid-template-columns: 1fr;
      gap: 30px;
    }

    @include responsive(mobile) {
      grid-template-columns: 1fr;
      gap: 20px;
    }
  }
}
</style>
