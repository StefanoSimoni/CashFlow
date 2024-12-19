<template>
  <li class="content">
    <div class="left">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
    </div>
    <div class="right">
      <img
        src="./../assets/trash-icon_5de37388-586f-4cb9-8ba9-1fabd994cb28.svg"
        alt="delete movement"
        @click="removeMovement(id)"
      />
      <h4 :style="{ color: isPositive }">{{ amountFormatted }}</h4>
    </div>
  </li>
</template>

<script setup>
import { toRefs, computed, defineEmits } from "vue";

const props = defineProps({
  id: {
    type: Number,
  },
  title: {
    type: String,
  },
  description: {
    type: String,
  },
  amount: {
    type: Number,
  },
});
const { id, title, description, amount } = toRefs(props);

const currencyFormatter = new Intl.NumberFormat("en-US", {
  style: "currency",
  currency: "USD",
});

const emits = defineEmits(["removeMovement"]);

const removeMovement = (id) => {
  emits("removeMovement", id);
};

const amountFormatted = computed(() => currencyFormatter.format(amount.value));
const isPositive = computed(() => (amount.value > 0 ? "#04b500" : "red"));
</script>

<style scoped>
.content {
  display: flex;
  justify-content: space-between;
  background-color: #c4e8f3;
  padding: 10px;
  border-radius: 5px;
}

.left {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.left h3 {
  color: #303233;
}

.right {
  display: flex;
  flex-direction: column;
  align-items: end;
  gap: 15px;
}

img {
  cursor: pointer;
}
</style>
