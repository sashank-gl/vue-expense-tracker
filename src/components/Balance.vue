<script setup>
import { defineProps } from 'vue';

const props = defineProps({
    totalBalance: {
        type: Number, required: true
    }
})
</script>

<template>
    <div class="text-xl flex gap-2">
        <h3>Current Balance: </h3>
        <p id="balance">$ {{ totalBalance }}</p>
    </div>
</template>