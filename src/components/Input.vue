<script setup>
import { defineEmits, defineProps, ref, reactive, watch, onMounted, onUnmounted, computed } from "vue";

import Select from "./Select.vue";
import Button from "./Button.vue";

const emit = defineEmits(["update:modelValue", "action", "changed"]);
const props = defineProps({
    placeholder: {},
    id: {},
    name: {},
    label: null,
    value: {},
    relations: {},
    options: {},
    background: {},
    color: {},
    modelValue: {},
    disabled: {},
    postFix: {},
    type: {
        default: "text"
    },
    selectLabel: "",
    min: '',
    max: ''
});
const internal = ref("");
const focus = ref(false);

const checkboxOptions = [
    {
        value: 0,
        name: "No"
    },
    {
        value: 1,
        name: "Si"
    },
]
const Update = (value) => {
    internal.value = value;
    emit("update:modelValue", value);
}
const setFocus = (state) => {
    focus.value = state;
}
const Translation = (string) => {
    return string;
}
const action = () => {
    emit("action");
}

onMounted(() => {
    internal.value = props.value;
})

watch(internal, (val) => {
    emit("update:modelValue", val);
    emit("changed", { value: val, key: props.label });
})
watch(() => props.modelValue, (newValue) => {
    internal.value = newValue;
}, { immediate: true });

</script>

<template>
    <div class="custom-input" flex-start flex-column>
        <label v-if="label" :for="name" :class="{ focused: focus }">{{ label }}</label>
        <Select v-if="type === 'select'" :placeholder :id :name :value :label="selectLabel"
            :options="options ?? relations" v-model="internal" @focusin="setFocus(true)" @focusout="setFocus(false)"
            @update="Update" customselect />
        <Select v-else-if="type === 'select_checkbox'" :placeholder :id :name :value :options="checkboxOptions"
            v-model="internal" @update="Update" @focusin="setFocus(true)" @focusout="setFocus(false)" customselect />
        <textarea v-else-if="type === 'textarea'" v-on:focus="setFocus(true)" v-on:focusout="setFocus(false)"
            v-model="internal" :placeholder :id :name :type custominput />
        <Button v-else-if="type === 'button'" :value :type :id :background :color @action="action" />
        <input v-else v-on:focus="setFocus(true)" v-on:focusout="setFocus(false)" v-model="internal" :placeholder :id
            :name :type :min :max :disabled :style="{
                'background': background,
                'color': color
            }" custominput>
        </input>
    </div>
</template>

<style scoped>
input,
label {
    width: 100%;
}

input {
    padding: .6em 1em;
    transition: var(--duration);

    position: relative;

    background: var(--input-bg);
    color: var(--text-color);
}

textarea {
    width: 100%;
    height: 200px;
    padding: 1em;
    resize: none;
}

label {
    margin-bottom: 1em;
    color: var(--text-color);
    transition: var(--duration);
}

.focused {
    color: var(--primary);
}
</style>