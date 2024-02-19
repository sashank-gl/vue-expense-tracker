<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import AddTransaction from './components/AddTransaction.vue';
import TransactionList from './components/TransactionList.vue';
import { computed, onMounted, ref } from 'vue';
import { useToast } from 'vue-toastification'

const toast = useToast()
const transactions = ref([

])

onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'))
    if (savedTransactions) {
        transactions.value = savedTransactions
    }
})

const totalBalance = computed(() => {
    return transactions.value.reduce((total, transaction) => {
        return transaction.category === 'income'
            ? total + Number(transaction.amount)
            : transaction.category === 'expense'
                ? total - Number(transaction.amount)
                : total; // Handle unknown categories gracefully (e.g., log, return)
    }, 0);
});

const totalIncome = computed(() => {
    return transactions.value
        .filter(transaction => transaction.category === 'income')
        .reduce((total, transaction) => total + Number(transaction.amount), 0);
});

const totalExpense = computed(() => {
    return transactions.value
        .filter(transaction => transaction.category === 'expense')
        .reduce((total, transaction) => total + Number(transaction.amount), 0);
});

const handleTransactionAdded = (transactionData) => {
    transactions.value.push({ id: generateUniqueId(), item: transactionData.item, amount: transactionData.amount, category: transactionData.category })
    saveToLocal()
    toast.success('Item added')
}

const generateUniqueId = () => {
    return Math.floor(Math.random() * 10000)
}

const handleItemDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
    saveToLocal()
    toast.success('Item deleted')
}

const saveToLocal = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value))
}
</script>

<template>
    <div class="bg-[#e8e4e6] flex flex-col justify-center items-center h-screen">
        <div class="w-[32rem] bg-[#004643] text-[#fffffe] rounded-lg shadow-lg flex flex-col justify-center p-5 gap-4">
            <Header />
            <Balance :totalBalance="totalBalance" />
            <IncomeExpenses :totalIncome="totalIncome" :totalExpense="totalExpense" />
            <AddTransaction @transactionAdded="handleTransactionAdded" />
            <TransactionList :transactions="transactions" @itemDeleted="handleItemDeleted" />
        </div>
    </div>
</template>
