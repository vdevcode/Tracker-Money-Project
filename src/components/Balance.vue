<template>
  <div class="my-3">
    <p class="text-red-500">Đã chi tiêu: {{ totalAmount.toFixed(3) }} vnđ</p>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
const props = defineProps({
  totalAmount: {
    type: Number,
    required: true,
  },
});
</script>
