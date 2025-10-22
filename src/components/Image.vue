<template>
    <div class="image-container" :style="{ width: width, height: height }">
        <img :src="src" :alt="alt" :width="width" :height="height" crossorigin="anonymous" @error="$emit('error')"
            @load="load($event)" />
    </div>
</template>

<script setup>
const emits = defineEmits(['error', 'load']);
const props = defineProps({
    src: {
        type: String,
        required: true
    },
    alt: {
        type: String,
        default: ''
    },
    width: {
        type: [String, Number],
        default: 'auto'
    },
    height: {
        type: [String, Number],
        default: 'auto'
    }
});

async function load(evt) {
    const elem = evt.target;
    const parent = elem.parentElement;
    const color = getDominantColor(elem);

    parent.style.backgroundColor = color;
    emits('load', evt, color)
}

function getDominantColor(imgEl) {
    const canvas = document.createElement("canvas");
    canvas.width = imgEl.naturalWidth;
    canvas.height = imgEl.naturalHeight;
    const ctx = canvas.getContext("2d");
    ctx.drawImage(imgEl, 0, 0);

    const imageData = ctx.getImageData(0, 0, canvas.width, canvas.height);
    const data = imageData.data;
    const colorCount = {};
    let maxCount = 0;
    let dominantColor = [255, 255, 255];

    // Sample every 20th pixel for performance
    for (let i = 0; i < data.length; i += 80) {
        const r = data[i];
        const g = data[i + 1];
        const b = data[i + 2];
        // Ignora píxeles muy claros (blancos)
        // if (r > 240 && g > 240 && b > 240) continue;
        const key = `${r},${g},${b}`;
        colorCount[key] = (colorCount[key] || 0) + 1;
        if (colorCount[key] > maxCount) {
            maxCount = colorCount[key];
            dominantColor = [r, g, b];
        }
    }

    return `rgb(${dominantColor[0]},${dominantColor[1]},${dominantColor[2]})`;
}
</script>

<style scoped>
img {
    object-fit: contain;
}
</style>