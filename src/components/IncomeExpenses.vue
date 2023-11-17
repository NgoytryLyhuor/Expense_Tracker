<template>
    <div class="row" style="margin-top: -60px;">
        <div class="col-xl-3 col-md-6">
            <div class="card">
                <div class="card-body">
                    <div class="row">
                        <div class="col-6 text-center">
                            <div class="d-flex">
                                <div class="flex-grow-1">
                                    <p class="text-truncate font-size-14 mb-2">Income</p>
                                    <h4 class="mb-2 text-success">${{ income }}</h4>
                                </div>
                            </div>
                        </div>
                        <div class="col-6 text-center">
                            <div class="d-flex">
                                <div class="flex-grow-1">
                                    <p class="text-truncate font-size-14 mb-2">Expense</p>
                                    <h4 class="mb-2 text-danger">${{ expenses }}</h4>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- end cardbody -->
            </div>
            <!-- end card -->
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expenses: {
        type: Number,
        required: true
    }
});
</script>