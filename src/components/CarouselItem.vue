<script setup>
import { defineProps } from "vue";
const props = defineProps({
    active: false,
    text: "",
});
</script>

<template>
    <div :class="{ 'carousel-item': true, 'active': active }">
        <slot></slot>
        <pre>
            <div v-if="text" class="text" v-html="text"></div>
        </pre>
    </div>
</template>

<style scoped>
.carousel-item {
    height: 100%;
    position: relative;

    &>.text {
        top: 50%;
        left: 50%;
        position: absolute;
        transform: translate(-50%, -50%);

        color: white;
        text-shadow: 0px 0px 15px black;

        user-select: none;
        text-align: center;

        background: rgba(0, 0, 0, 0.5);
        padding: 1em 2em;
    }
}
</style>