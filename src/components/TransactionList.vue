<script setup>
const { transactions } = defineProps({
  transactions: Object,
});

const emit = defineEmits(["onDelete"]);
const onDelete = (id) => {
  emit("onDelete", id);
};
</script>

<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      v-for="transaction in transactions"
      :key="transaction.id"
      :class="[transaction.amount > 0 ? 'plus' : 'minus']"
    >
      {{ transaction.text }}
      <span> {{ transaction.amount }}</span>
      <button class="delete-btn" @click="onDelete(transaction.id)">
        x
      </button>
    </li>
  </ul>
</template>
