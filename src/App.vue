<script setup>
import { defineAsyncComponent } from "vue";
import Splashscreen from "./components/Splashscreen.vue";

const Home = defineAsyncComponent(
  () =>
    new Promise((res) =>
      setTimeout(() => res(import("./components/Home.vue")), 2500)
    )
);
</script>

<template>
  <Suspense>
    <Home />
    <template #fallback>
      <Splashscreen />
    </template>
  </Suspense>
</template>

<style>
  * {
    margin: 0;
    font-family: Arial, Helvetica, sans-serif;
  }
</style>
