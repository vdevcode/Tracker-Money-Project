<template>
    <div class="flex items-center justify-between gap-4 w-[100%] rounded-md p-4 text-center bg-black text-white">
        <div class="border border-green-400 p-3">
            <h4>Thu nhập</h4>
            <p class="text-green-400">+{{ income.toFixed(3) }}vnđ</p>
        </div>
        <div  class="border border-red-500 p-3">
            <h4>Chi phí</h4>
            <p class="text-red-400">{{ expense.toFixed(3) }}vnđ</p>
        </div>
    </div>
</template>

<script setup>

import {defineProps} from "vue"

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense: {
        type: Number,
        required: true
    }
})

</script>