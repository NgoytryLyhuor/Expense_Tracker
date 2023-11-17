<template>
    <div class="row">
        <div class="col-12">
            <h3>Add new transaction</h3>
            <div class="card">
                <div class="card-body">
                    <!-- end row -->
                    <form @submit.prevent="onSubmit">
                        <div class="row mb-3">
                            <div class="col-sm-10">
                                <input class="form-control" v-model="text" type="search" placeholder="text">
                            </div>
                        </div>
                        <!-- end row -->
                        <div class="row mb-3">
                            <div class="col-sm-10">
                                <input class="form-control" v-model="amount" type="text" placeholder="amount">
                            </div>
                        </div>
                        <button class="btn btn-success">Add transaction</button>

                    </form>

                </div>
            </div>
        </div> <!-- end col -->
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification'
const text = ref('');
const amount = ref('');
const toast = useToast();
const emit = defineEmits(['transactionSubmitted'])

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error('Both Fields must be filled.');
        return;
    }
    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value),
    }
    emit('transactionSubmitted', transactionData);
    text.value = '';
    amount.value = '';
};
</script>