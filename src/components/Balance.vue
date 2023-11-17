<template>
    <div class="container-fluid" style="float: left; width: 100%; margin-bottom: 20px;">
        <div class="left" style="float: left;">
        <h4>Balance in Dollar</h4>
        <h1 id="balance">${{ total }}</h1>
    </div>
    <div class="right" style="float: right;">
        <h4>Balance in riel</h4>
        <h1 id="balance">{{ totalInRiel }}៛</h1>
    </div>
    </div>
</template>

<script setup>
import { defineProps } from 'vue';
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