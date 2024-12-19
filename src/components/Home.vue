<template>
  <Layout>
    <template #header><Header /></template>
    <template #resume
      ><Resume :totalAmount="123" :amountDate="123"
        ><template #addMovement><AddMovementButton /></template></Resume
    ></template>
    <template #history><History :movements="movements" /></template>
  </Layout>
</template>

<script setup>
import { ref } from "vue";
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume.vue";
import AddMovementButton from "./AddMovementButton.vue";
import History from "./History.vue";

const movements = ref([
  {
    id: 0,
    title: "Movement 1",
    description: "Description for Movement 1",
    amount: 123456,
  },
  {
    id: 1,
    title: "Movement 2",
    description: "Description for Movement 2",
    amount: 123456,
  },
  {
    id: 2,
    title: "Movement 3",
    description: "Description for Movement 3",
    amount: 123456,
  },
  {
    id: 3,
    title: "Movement 4",
    description: "Description for Movement 4",
    amount: -123456,
  },
]);
</script>

<style scoped></style>
