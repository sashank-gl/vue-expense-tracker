<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification'

const toast = useToast()
const item = ref('')
const amount = ref('')
const category = ref('')
const emit = defineEmits(['transactionAdded'])

const onSubmit = () => {
    if (!item.value || !amount.value || !category.value) {
        toast.error('Fields should not be empty')
    }

    const numberRegex = /^\d+(\.\d+)?$/;
    if (!numberRegex.test(amount.value)) {
        toast.error('Amount should be a number');
    }

    const transactionData = {
        item: item.value,
        amount: parseFloat(amount.value),
        category: category.value,
    }

    emit('transactionAdded', transactionData)
    
    console.log(transactionData)
    item.value = ''
    amount.value = ''
    category.value = 'income';
}
</script>

<template>
    <h2 class="text-xl">Add Transaction</h2>
    <form id="form" @submit.prevent="onSubmit">
        <div class="text-xl flex flex-col gap-2 text-[#001e1d]">
            <input class="p-2 rounded-lg" v-model="item" type="text" id="item" placeholder="Enter Item" />
            <input class="p-2 rounded-lg" v-model="amount" type="number" id="amount" placeholder="Enter Amount" />
            <div class="flex items-center gap-2">
                <label for="category">Category</label>
                <select class="p-2 rounded-lg" v-model="category">
                    <option value="">Select</option>
                    <option value="income">Income</option>
                    <option value="expense">Expense</option>
                </select>
            </div>

            <button class="bg-[#f9bc60] font-semibold py-2 px-4 rounded-lg">Add</button>
        </div>
    </form>
</template>