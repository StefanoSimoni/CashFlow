<template>
  <div class="modal">
    <header>
      <p>New Movement</p>
      <img
        src="./../assets/close-icon_039b6837-d928-4f74-a2e9-7953715dbfd8.svg"
        alt="close modal"
        @click="closeModal"
      />
    </header>
    <main><slot></slot></main>
  </div>
</template>

<script setup>
const emits = defineEmits(["closeModal"]);

const closeModal = () => emits("closeModal");
</script>

<style scoped>
.modal {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 2;
  background-color: white;
}

header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
}

header p {
  font-size: x-large;
  color: #0689b0;
}

header img {
  cursor: pointer;
}
</style>
