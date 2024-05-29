<script setup>
import { ref, defineProps, onBeforeMount } from "vue";
const props = defineProps(["width"])
const style = ref("");
onBeforeMount(() => {
    style.value = `grid-template-columns: repeat(auto-fill, ${props.width}px);`;
})
</script>

<template>
    <div class="dp-grid" :style>
        <slot>

        </slot>
    </div>
</template>

<style scoped>
.dp-grid {
    display: grid;
    justify-content: space-around;
}
</style>