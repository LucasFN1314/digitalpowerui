<script setup>
import { defineProps } from "vue";
const props = defineProps(["title", "maxWidth"]);
</script>
<template>
    <div class="dp-container" :style="{
        'max-width': `${maxWidth}px`
    }">
        <h1 underline>{{ title }}</h1>
        <slot></slot>
    </div>
</template>

<style scoped>
h1 {
    width: fit-content;
}

.dp-container {
    width: 100%;
    height: 100%;
    padding: 2em;
    margin: auto;
    overflow-y: auto;
}
</style>