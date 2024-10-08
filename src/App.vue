<script setup>
//imports
import Balance from "./components/Balance.vue";
import Header from "./components/Header.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { computed, ref } from "vue";
// refs
const transactions = ref([
  {
    id: 1,
    text: "salary",
    amount: 1600,
  },
  {
    id: 2,
    text: "Chéque",
    amount: 500,
  },
  {
    id: 3,
    text: "Rent",
    amount: -750,
  },
]);
// computed
const balance = computed(() => {
  return transactions.value.reduce((prev, current) => {
    return prev + current.amount;
  }, 0);
});
const income = computed(() => {
  return transactions.value.reduce((prev, current) => {
    return current.amount > 0 ? prev + current.amount : prev;
  }, 0);
});
const expense = computed(() => {
  return transactions.value.reduce((prev, current) => {
    return current.amount < 0 ? current.amount + prev : prev;
  }, 0);
});

// methods
const handleAddTransaction = (newTransaction) => {
  const transactionWithId = {
    id: Date.now(),
    ...newTransaction,
  };
  transactions.value.push(transactionWithId);
};

const handleDelete = (id) => {
  transactions.value = transactions.value.filter((transaction) => {
    return transaction.id !== id;
  });
};

</script>

<template>
  <Header />
  <div class="container">
    <Balance :balance="balance" />
    <IncomeExpenses :expense="expense" :income="income" />
    <TransactionList :transactions="transactions" @onDelete="handleDelete" />
    <AddTransaction @add="handleAddTransaction" />
  </div>
</template>
