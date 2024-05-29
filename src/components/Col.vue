<script setup>
import { defineProps } from "vue";
const props = defineProps(["col", "xs", "sm", "md", "lg", "xl"]);
</script>
<template>
    <div :class="{
        'col': true,
        [`col-${props.col}`]: true,
        [`col-xs-${props.xs}`]: true,
        [`col-sm-${props.sm}`]: true,
        [`col-md-${props.md}`]: true,
        [`col-lg-${props.lg}`]: true,
        [`col-xl-${props.xl}`]: true
    }">
        <slot></slot>
    </div>
</template>