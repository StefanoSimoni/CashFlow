<template>
  <Layout>
    <template #header><Header /></template>
    <template #resume
      ><Resume :totalAmount="123" :amountDate="123"
    /></template>
    <template #history><History /></template>
  </Layout>
</template>

<script setup>
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume.vue";
import History from "./History.vue";
</script>

<style scoped></style>
