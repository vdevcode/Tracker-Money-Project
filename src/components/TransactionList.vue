<template>
  <div class="mt-4 mb-2 border-b-[2px] border-black">
    <p>Lịch sử</p>
  </div>
  <div class="">
    <ul>
      <li
        v-for="transaction in transactions"
        v-bind:key="transaction.id"
        class="flex my-2 items-center justify-between bg-black text-white p-2 rounded-md"
      >
        <span>{{ transaction.text }}</span>
        <p>{{ transaction.amount }}vnd</p>
        <div
          class="w-2 h-8 cursor-pointer relative show-button"
          :class="transaction.amount < 0 ? 'bg-red-400 ' : 'bg-green-400'"
        >
          <button
            :class="transaction.amount < 0 ? 'bg-red-400 ' : 'bg-green-400'"
            class="absoblute r-0 t-0 py-1 px-2 rounded-md hidden"
            @click="deletedTransaction(transaction.id)"
          >
            x
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps } from "vue";
const emit = defineEmits(['deletedTransaction'])
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deletedTransaction = (id) =>{
    emit('deletedTransaction', id)
}

</script>
