<script setup>
import { defineEmits, defineProps, ref, reactive, watch, onMounted, onUnmounted, computed } from "vue";

const emit = defineEmits(["action"])
const props = defineProps(["value", "type", "background", "color", "disabled"])
const action = () => {
  emit("action");
}
</script>

<template>
  <div class="custom-button">
    <button :disabled :type :style="{ background: background, color: color }" @click="action">{{ value }}</button>
  </div>
</template>

<style scoped>
button {
  display: block;
  width: fit-content;
  padding: .6em 1.5em;

  border-radius: 5px;
  border: none;

  cursor: pointer;
  font-size: 1em;

  transition: var(--duration);
  background: var(--input-button);
  color: var(--text-color);

  &:hover {
    background: var(--input-bg-hover);
  }

  &:focus {
    outline: none;
  }
}
</style>