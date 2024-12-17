<template>
  <Layout>
    <template #header><Header /></template>
    <template #resume><Resume :totalAmount="123" :amountDate="123" /></template>
    <template #history><History :movements="movements" /></template>
  </Layout>
</template>

<script setup>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume.vue";
import History from "./History.vue";

const movements = [
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
];
</script>

<style scoped></style>
