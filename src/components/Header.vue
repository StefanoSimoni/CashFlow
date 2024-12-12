<template>
  <header>
    <img
      src="./../assets/cashflow-icon_070076db-e83a-4afa-b18d-ee058c2b646e.svg"
      alt="cashflow icon"
      @click="reload"
    />
    <h1>Cash<span>Flow</span></h1>
    <span></span>
  </header>
</template>

<script setup>
const reload = () => {
  location.reload();
};
</script>

<style scoped>
header {
  width: 100vw;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
  padding: 10px 0 10px 0;
}

img {
  width: 40px;
  cursor: pointer;
}

h1 {
  color: #04b500;
}

span {
  color: #0689b0;
}
</style>
