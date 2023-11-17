<template>
    <div class="col-xl-8" style="margin-top: -100px;">
        <h4 style="margin-bottom: 12px;">History</h4>
    
        <div v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount > 0 ? 'alert alert-success alert-dismissible' : 'alert alert-danger alert-dismissible' " style="margin-top: -13px;">
            {{ transaction.text }}  <span class="float-end">${{ transaction.amount }}</span>
            <button @click="deleteTransaction(transaction.id)" class="btn-close" ></button>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue'
const emit = defineEmits(['transactionDeleted']);
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
})

const deleteTransaction = (id) => {
    emit('transactionDeleted', id)
};

</script>