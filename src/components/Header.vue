<template>
    <div class="flex justify-center items-center gap-2">
        <img :src="logo" alt="Expense Tracker Logo" class="w-16" />
        <h1 class="text-3xl text-center underline font-semibold">Expense Tracker</h1>
    </div>
</template>

<script>
import logo from "../assets/wallet.png"
export default {
    data: function () {
        return { logo: logo }
    }
}
</script>