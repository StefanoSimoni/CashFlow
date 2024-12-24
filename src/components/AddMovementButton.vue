<template>
  <button @click="showModal = true">Add Movement</button>
  <teleport to="#app">
    <Modal v-show="showModal" @closeModal="showModal = false">
      <template #default
        ><FormAddMovement @closeModal="showModal = false" /></template></Modal
  ></teleport>
</template>

<script setup>
import { ref } from "vue";
import Modal from "./Modal.vue";
import FormAddMovement from "./FormAddMovement.vue";

const showModal = ref(false);
</script>

<style scoped>
button {
  color: white;
  background-color: #0689b0;
  border: none;
  border-radius: 50px;
  padding: 20px 60px;
  font-size: large;
  cursor: pointer;
}
</style>
