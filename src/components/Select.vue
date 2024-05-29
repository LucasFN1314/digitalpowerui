<script setup>
import { defineEmits, defineProps, ref, reactive, watch, onMounted, onUnmounted, computed } from "vue";

const props = defineProps({
    id: "",
    name: "",
    options: Array,
    modelValue: {},
    label: null,
});

const internal = ref(null);
const emit = defineEmits(["update", "focusin", "focusout"])
watch(internal, (val) => {
    emit("update", val);
});
watch(() => props.modelValue, (newValue) => {
    internal.value = (newValue) ? newValue : null;
}, { immediate: true });
</script>

<template>
    <div class="select-wrapper">
        <select v-model="internal" v-on:focus="emit('focusin')" v-on:focusout="emit('focusout')" custominput>
            <option :value="null">{{ label ?? 'Seleccione una opcion' }}</option>
            <option v-for="(option, index) in options" :key="index" :value="option?.value">
                {{ option?.name }}
            </option>
        </select>
    </div>
</template>
<style scoped>
select {
    background: var(--input-bg);
    color: var(--text-color);
}
</style>