<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="addTransaction">
    <div class="form-control">
      <label for="text">Text</label>
      <input
        type="text"
        id="text"
        placeholder="Enter text..."
        v-model="newTransaction.text"
      />
    </div>
    <div class="form-control">
      <label for="amount">
        Amount <br />
        (negative - expense, positive - income)
      </label>
      <input
        type="number"
        id="amount"
        placeholder="Enter amount..."
        v-model.number="newTransaction.amount"
      />
    </div>
    <button type="submit" class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits(["add"]);
const newTransaction = ref({
  text: "",
  amount: null,
});

const addTransaction = () => {
  emit("add", { ...newTransaction.value });
  newTransaction.value.text = "";
  newTransaction.value.amount = null;
};
</script>
