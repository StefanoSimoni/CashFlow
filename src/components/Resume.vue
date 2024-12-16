<template>
  <main>
    <p>{{ label }}</p>
    <h1>{{ amountFormatted }}</h1>
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
const amountFormatted = computed(() => amountFormatter.format(amount.value));
</script>

<style scoped>
p {
  text-align: center;
}

h1 {
  text-align: center;
  color: #04b500;
}
</style>
