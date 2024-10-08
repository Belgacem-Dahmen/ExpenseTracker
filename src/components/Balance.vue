<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{ props.balance }}</h1>
</template>

<script setup>
const props = defineProps({
  balance: Number,
});
</script>
