<template>
  <Layout>
    <template #header><Header /></template>
    <template #resume
      ><Resume :totalAmount="123" :amountDate="123"
        ><template #addMovement><AddMovementButton /></template
        ><template #graphic><Graphic :amounts="amounts" /></template></Resume
    ></template>
    <template #history
      ><History :movements="movements" @save="save"
    /></template>
  </Layout>
</template>

<script setup>
import { computed, onMounted, provide, ref } from "vue";
import Layout from "./Layout.vue";
import Header from "./Header.vue";
import Resume from "./Resume.vue";
import Graphic from "./Graphic.vue";
import AddMovementButton from "./AddMovementButton.vue";
import History from "./History.vue";

const movements = ref([]);

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

onMounted(() => {
  const movementsLS = JSON.parse(localStorage.getItem("movements"));

  if (Array.isArray(movementsLS)) {
    movements.value = movementsLS.map((movement) => {
      return { ...movement, date: new Date(movement.date) };
    });
  }
});

const save = () => {
  localStorage.setItem("movements", JSON.stringify(movements.value));
};

provide("movements", { movements, save });
</script>

<style scoped></style>
