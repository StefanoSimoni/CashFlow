<template>
  <main>
    <div>
      <p>{{ label }}</p>
      <h1 :style="{ color: isPositive }">{{ amountFormatted }}</h1>
    </div>
    <slot name="graphic"></slot>
    <slot name="addMovement"></slot>
  </main>
</template>

<script setup>
import { computed, toRefs } from "vue";

const currencyFormatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});

const props = defineProps({
  labelDate: {
    type: String,
  },
  totalAmount: {
    type: Number,
  },
  amountDate: {
    type: Number,
  },
});
const { labelDate, totalAmount, amountDate } = toRefs(props);

const label = computed(() =>
  labelDate.value ? labelDate.value : "Total Amount"
);
const amount = computed(() =>
  amountDate.value ? amountDate.value : totalAmount.value
);
const amountFormatted = computed(() => currencyFormatter.format(amount.value));
const isPositive = computed(() => (amount.value > 0 ? "#04b500" : "red"));
</script>

<style scoped>
p {
  text-align: center;
}

h1 {
  text-align: center;
}

main {
  height: 75vh;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
</style>
