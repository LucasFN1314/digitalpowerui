<script setup>
import { defineProps } from "vue";
const props = defineProps({
    id: "",
    blackArrows: "",
    interval: 0,
    hideArrows: false,
    activeSlide: Number,
    backgroundArrows: false,
});
</script>

<template>
    <div :id="id" class="carousel slide" data-bs-ride="carousel" :data-bs-interval="interval">
        <div class="carousel-inner">
            <slot></slot>
        </div>

        <div v-if="!hideArrows">
            <div v-if="blackArrows">
                <button class="carousel-control-prev black-arrows" type="button" :data-bs-target="`#${id}`"
                    data-bs-slide="prev">
                    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Previous</span>
                </button>
                <button class="carousel-control-next black-arrows" type="button" :data-bs-target="`#${id}`"
                    data-bs-slide="next">
                    <span class="carousel-control-next-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Next</span>
                </button>
            </div>
            <div v-else>
                <button :class="{ 'carousel-control-prev': true, 'backgroundArrows': backgroundArrows }" type="button"
                    :data-bs-target="`#${id}`" data-bs-slide="prev">
                    <span class="carousel-control-prev-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Previous</span>
                </button>
                <button :class="{ 'carousel-control-next': true, 'backgroundArrows': backgroundArrows }" type="button"
                    :data-bs-target="`#${id}`" data-bs-slide="next">
                    <span class="carousel-control-next-icon" aria-hidden="true"></span>
                    <span class="visually-hidden">Next</span>
                </button>
            </div>
        </div>
    </div>
</template>

<style scoped>
.carousel {
    height: 100%;

    &:hover {

        .carousel-control-next,
        .carousel-control-prev {
            opacity: 100%;
        }
    }
}

.carousel-inner {
    height: 100%;
}

.carousel-control-next,
.carousel-control-prev {
    transition: .2s;
    opacity: 0;
}

.black-arrows .carousel-control-next-icon {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='black'%3e%3cpath d='M4.646 1.646a.5.5 0 0 1 .708 0l6 6a.5.5 0 0 1 0 .708l-6 6a.5.5 0 0 1-.708-.708L10.293 8 4.646 2.354a.5.5 0 0 1 0-.708z'/%3e%3c/svg%3e") !important;
}

.black-arrows .carousel-control-prev-icon {
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16' fill='black'%3e%3cpath d='M11.354 1.646a.5.5 0 0 1 0 .708L5.707 8l5.647 5.646a.5.5 0 0 1-.708.708l-6-6a.5.5 0 0 1 0-.708l6-6a.5.5 0 0 1 .708 0z'/%3e%3c/svg%3e") !important;
}

.backgroundArrows {
    background: rgb(0, 0, 0, .5);
}

@media screen and (max-width: 1000px) {

    .carousel-control-next,
    .carousel-control-prev {
        opacity: 1;
    }
}
</style>