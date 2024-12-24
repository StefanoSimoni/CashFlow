<template>
  <Layout>
    <template #header><Header /></template>
    <template #resume
      ><Resume :totalAmount="123" :amountDate="123"
        ><template #addMovement><AddMovementButton /></template
        ><template #graphic><Graphic :amounts="amounts" /></template></Resume
    ></template>
    <template #history><History :movements="movements" /></template>
  </Layout>
</template>

<script setup>
import { computed, provide, ref } from "vue";
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume.vue";
import Graphic from "./Graphic.vue";
import AddMovementButton from "./AddMovementButton.vue";
import History from "./History.vue";

const movements = ref([
  {
    id: 0,
    title: "Movement 1",
    description: "Description for Movement 1",
    amount: 123456,
    date: new Date("12/10/2024"),
  },
  {
    id: 1,
    title: "Movement 2",
    description: "Description for Movement 2",
    amount: 123456,
    date: new Date("12/11/2024"),
  },
  {
    id: 2,
    title: "Movement 3",
    description: "Description for Movement 3",
    amount: 123456,
    date: new Date("12/12/2024"),
  },
  {
    id: 3,
    title: "Movement 4",
    description: "Description for Movement 4",
    amount: -123456,
    date: new Date("12/13/2024"),
  },
]);

provide("movements", movements);

const amounts = computed(() => {
  const lastDays = movements.value
    .filter((movement) => {
      const today = new Date();
      const oldDate = today.setDate(today.getDate() - 30);

      return movement.date > oldDate;
    })
    .map((movement) => movement.amount);

  return lastDays.map((amount, i) => {
    const lastAmount = lastDays.slice(0, i + 1);

    return lastAmount.reduce((sum, amount) => sum + amount, 0);
  });
});
</script>

<style scoped></style>
