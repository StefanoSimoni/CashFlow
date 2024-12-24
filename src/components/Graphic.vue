<template>
  <div>
    <svg
      viewBox="0 0 300 200"
      @touchstart="tap"
      @touchmove="tap"
      @touchend="unTap"
    >
      <line
        stroke="#c4c4c4"
        stroke-width="2"
        x1="0"
        :y1="zero"
        x2="300"
        :y2="zero"
      />
      <polyline
        fill="none"
        stroke="#0689b0"
        stroke-width="2"
        :points="points"
      />
      <line
        v-show="showPointer"
        stroke="#04b500"
        stroke-width="2"
        :x1="pointer"
        y1="0"
        :x2="pointer"
        y2="200"
      />
    </svg>
    <p>Last 30 days</p>
  </div>
</template>

<script setup>
import { toRefs, computed, ref } from "vue";

const props = defineProps({
  amounts: {
    type: Array,
  },
});

const { amounts } = toRefs(props);

const amountToPixels = (amount) => {
  const min = Math.min(...amounts.value);
  const max = Math.max(...amounts.value);

  const amountAbs = amount + Math.abs(min);
  const minmax = Math.abs(max) + Math.abs(min);

  return 200 - ((amountAbs * 100) / minmax) * 2;
};

const zero = computed(() => {
  return amountToPixels(0);
});

const points = computed(() => {
  const total = amounts.value.length;
  return amounts.value.reduce((points, amount, i) => {
    const x = (300 / total) * (i + 1);
    const y = amountToPixels(amount);
    return `${points} ${x},${y}`;
  }, "0, 100");
});

const showPointer = ref(false);
const pointer = ref(0);

const tap = (e) => {
  showPointer.value = true;
  const elementWidth = e.target.getBoundingClientRect().width;
  const elementX = e.target.getBoundingClientRect().x;
  const touchX = e.touches[0].clientX;
  pointer.value = ((touchX - elementX) * 300) / elementWidth;
};

const unTap = () => (showPointer.value = false);
</script>

<style scoped>
svg {
  width: 100%;
}

p {
  text-align: center;
}
</style>
