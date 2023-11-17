<template>
    <div class="row">
        <div class="col-6">
            <div class="d-flex">
                <div class="flex-grow-1">
                    <h5 class="text-truncate mb-2">Balance in Dollar</h5>
                    <h2 class="mb-2">${{ total }}</h2>
                </div>
            </div>
        </div>
        <div class="col-6">
            <div class="d-flex">
                <div class="flex-grow-1">
                    <h5 class="text-truncate mb-2">Balance in riel</h5>
                    <h2 class="mb-2">{{ totalInRiel }}៛</h2>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
import { component as VueNumber } from '@coders-tm/vue-number-format'

const props = defineProps({
    total: {
        type: Number,
        required: true
    },
    totalInRiel: {
        type: Number,
        required: true
    }
});

</script>