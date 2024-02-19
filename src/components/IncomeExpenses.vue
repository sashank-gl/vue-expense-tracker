<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    totalIncome: {
        type: Number, required: true
    },
    totalExpense: {
        type: Number, required: true
    }
})
</script>

<template>
    <div class="flex w-full">
        <div class="w-1/2 flex flex-col justify-center items-center gap-2 bg-[#abd1c6] text-[#001e1d] py-2">
            <h3 class="font-semibold">Income</h3>
            <p id="income" class="font-bold">$ {{ totalIncome }}</p>
        </div>
        <div class="w-1/2 flex flex-col justify-center items-center gap-2 bg-[#f9bc60] text-[#001e1d] py-2">
            <h3 class="font-semibold">Expense</h3>
            <p id="expense" class="font-bold">$ {{ totalExpense }}</p>
        </div>
    </div>
</template>