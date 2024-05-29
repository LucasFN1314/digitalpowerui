<script setup>
import { onBeforeMount, onMounted, defineProps, defineEmits } from "vue";
const props = defineProps({
    width: {
        default: "unset"
    },
    class: "",
    id: "",
    title: "",
});

const emit = defineEmits(["close"]);

onBeforeMount(() => {
    window.removeEventListener("click", clickOutsideHandler);
});
onMounted(() => {
    setTimeout(() => {
        window.addEventListener("click", clickOutsideHandler);
    }, 300)
});

const clickOutsideHandler = () => {
    var elem = document.querySelector(".custom-modal");
    if (
        elem?.classList?.contains("custom-modal") &&
        !elem.contains(event.target)
    ) {
        emit("close");
    }
};
</script>

<template>
    <div overlay fade></div>
    <div class="custom-modal p-5" :class :id shadow fade radius-border>
        <div class="row mb-5 pb-3 title">
            <h5>
                {{ title }}
            </h5>
        </div>
        <div class="row">
            <slot></slot>
        </div>
    </div>
</template>

<style scoped>
.custom-modal {
    max-height: 100vh;
    max-width: 100vh;
    position: fixed;
    top: 50%;
    left: 50%;
    z-index: 200000;
    background: var(--back-color);
    color: var(--text-color) !important;
    overflow-y: auto;

    width: 90%;
    max-width: 600px;

    transform: translate(-50%, -50%);

    &>.title {
        border-bottom: 1px solid var(--gray);

        &>h5 {
            text-align: center;
        }
    }
}
</style>