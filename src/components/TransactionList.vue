<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    transactions: {
        type: Array, required: true
    }
})

const emit = defineEmits(['itemDeleted'])
const deleteItem = (id) => {
    emit('itemDeleted', id)
}
</script>

<template>
    <div>
        <h2 class="text-xl mb-6">History</h2>
        <div class="overflow-y-auto h-48">
            <ul id="list" class="flex flex-col gap-2">
                <li :key="transaction.id" v-for="transaction in transactions" class="grid grid-cols-4 gap-5"
                    :class="transaction.category === 'income' ? 'border-l-4 border-teal-500' : 'border-l-4 border-orange-500'">
                    <p class="col-span-2">{{ transaction.item }}</p>
                    <p>$ {{ transaction.amount }}</p>
                    <!-- <p>{{ transaction.category }}</p> -->
                    <button @click="deleteItem(transaction.id)" class="py-2 px-4 rounded-md bg-red-500 mr-2">Delete</button>
                </li>
            </ul>
        </div>
    </div>
</template>