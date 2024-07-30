<template>
    <div class="overlayedCard" flex-center radius-border @click="action">
        <img :src="img" alt="">
        <p>{{ text }}</p>
    </div>
</template>

<script setup>
    const props = defineProps(["img", "text"]);
    const emits = defineEmits(["action"]);
    const action = () => {
        emits("action");
    }
</script>

<style scoped lang="scss">
.overlayedCard {
    cursor: pointer;
    width: 128px;
    height: 200px;
    position: relative;

    img {
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
    }

    &::after {
        content: "";
        width: 100%;
        height: 100%;
        position: absolute;
        top: 0;
        left: 0;
        opacity: 0;
        transition: var(--duration);
    }

    &:hover::after {
        opacity: 1;
    }
}
</style>