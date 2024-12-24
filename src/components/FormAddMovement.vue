<template>
  <form ref="addMovement" @submit.prevent="createMovement">
    <div>
      <label for="title">Title</label>
      <input type="text" name="title" id="title" v-model="title" required />
    </div>
    <div>
      <label for="amount">Amount</label>
      <input
        type="number"
        name="amount"
        id="amount"
        min="1"
        v-model="amount"
        required
      />
    </div>
    <div>
      <label for="description">Description</label>
      <textarea
        name="description"
        id="description"
        rows="8"
        v-model="description"
        required
      ></textarea>
    </div>
    <div>
      <label for="entry" class="movementType">
        Entry
        <input
          type="radio"
          name="radio"
          id="entry"
          value="Entry"
          v-model="movementType"
          required
        />
        <span class="checkmark"></span>
      </label>
      <label for="spent" class="movementType">
        Spent
        <input
          type="radio"
          name="radio"
          id="spent"
          value="Spent"
          v-model="movementType"
          required
        />
        <span class="checkmark"></span>
      </label>
    </div>
    <div>
      <button type="submit">Add Movement</button>
    </div>
  </form>
</template>

<script setup>
import { inject, ref } from "vue";

const addMovement = ref(null);

const { movements, save } = inject("movements");

let title = ref("");
let amount = ref(null);
let description = ref("");
let movementType = ref("");

const emits = defineEmits(["closeModal"]);

const createMovement = () => {
  emits("closeModal");

  movements.value.push({
    id: movements.value.length,
    title: title.value,
    amount: movementType.value === "Entry" ? amount.value : -amount.value,
    description: description.value,
    date: new Date(),
  });

  save();

  resetForm();
};

const resetForm = () => {
  title.value = "";
  amount.value = null;
  description.value = "";
  addMovement.value.reset();
};
</script>

<style scoped>
form {
  padding: 0 20px 20px 20px;
  background-color: white;
}

div {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

form div:nth-child(n + 2) {
  padding-top: 50px;
}

label {
  font-size: x-large;
}

input,
textarea {
  border: 2px solid #0689b0;
  border-radius: 5px;
  padding: 10px;
  font-size: large;
}

.movementType {
  display: block;
  position: relative;
  padding-left: 35px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size: 22px;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

.movementType input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color: white;
  border: 2px solid #0689b0;
  border-radius: 50%;
}

.movementType:hover input ~ .checkmark {
  background-color: #93d0e2;
}

.movementType input:checked ~ .checkmark {
  background-color: #0689b0;
}

.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

.movementType input:checked ~ .checkmark:after {
  display: block;
}

.movementType .checkmark:after {
  top: 9px;
  left: 9px;
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: white;
}

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
