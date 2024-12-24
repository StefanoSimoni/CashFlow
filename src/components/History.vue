<template>
  <ul>
    <Movement
      v-for="movement in movements"
      :key="movement.id"
      :id="movement.id"
      :title="movement.title"
      :description="movement.description"
      :amount="movement.amount"
      @removeMovement="removeMovement"
    />
  </ul>
</template>

<script setup>
import { toRefs } from "vue";
import Movement from "./Movement.vue";

const props = defineProps({
  movements: {
    type: Array,
  },
});
const { movements } = toRefs(props);

const emits = defineEmits(["save"]);

const removeMovement = (id) => {
  const index = movements.value.findIndex((movement) => movement.id === id);

  movements.value.splice(index, 1);
  movements.value.forEach((movement, id) => (movement.id = id));

  emits("save");
};
</script>

<style scoped>
ul {
  text-decoration: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
  gap: 10px;
}
</style>
