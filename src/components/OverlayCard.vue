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
    overflow: hidden;
    color: var(--font);
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
        object-fit: cover;
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
        background: rgba(0, 0, 0, 0.6);
    }

    &:hover {
        p {
            opacity: 1 !important;
        }
    }

    &:hover::after {
        opacity: 1;
    }
}

.overlayedCard>p {
    color: var(--font);
    width: 80%;
    opacity: 0;
    z-index: 10 !important;
    transition: var(--duration);
}
</style>