<script setup>
import { onMounted, defineEmits } from "vue";
const emit = defineEmits(["action"])
onMounted(() => {
    const area = document.getElementById("fileDrop");

    area.addEventListener('dragover', (event) => {
        event.preventDefault();
    });

    area.addEventListener('dragleave', () => {
    });

    area.addEventListener('click', () => {
        let selector = document.createElement("input");
        selector.setAttribute("id", "fileSelector");
        selector.type = "file";
        selector.multiple = true;
        document.body.appendChild(selector);
        selector.click();

        selector.addEventListener("change", (event) => {
            event.preventDefault();
            emit("action", event.target.files);
            selector.remove();
        });
    });

    area.addEventListener("drop", (event) => {
        event.preventDefault();
        emit("action", event.dataTransfer.files);
    })
})
</script>

<template>
    <div class="drop-area" id="fileDrop" radius-border shadow fade>
        <p absolute-centered>
            Haga click aqui o arrastre y suelte sus archivos.
        </p>
    </div>
</template>

<style scoped>
.drop-area {
    border: 1px solid var(--primary);
    width: 90%;
    height: 300px;
    padding: 1em;
    position: relative;
    margin: 2em auto;

    &>p {
        position: absolute;
        cursor: default;
        user-select: none;
        color: var(--text-color)
    }

}
</style>

<style>
#fileSelector {
    display: none;
}
</style>