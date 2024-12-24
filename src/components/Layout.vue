<template>
  <div class="layout">
    <slot name="header"></slot>
    <div v-show="!showHistory">
      <slot name="resume"></slot>
    </div>
    <div class="history">
      <div class="header" @click="showHistory = !showHistory">
        <span class="grip"></span>
      </div>
      <h1>History</h1>
      <div class="body" v-show="showHistory">
        <slot name="history"></slot>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const showHistory = ref(false);
</script>

<style scoped>
.layout {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  overflow-y: hidden;
}

.history {
  width: 100vw;
  box-shadow: #0689b0 0px 20px 70px;
  border-top-left-radius: 30px;
  border-top-right-radius: 30px;
  padding: 20px 0 0 0;
  display: flex;
  flex-direction: column;
}

h1 {
  padding-left: 20px;
  color: #0689b0;
}

.header {
  width: 100vw;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.grip {
  width: 30%;
  height: 10px;
  background-color: #93d0e2;
  border-radius: 10px;
}

.body {
  height: 70vh;
  padding: 20px;
  overflow-y: scroll;
}
</style>
