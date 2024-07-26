<template>
    <div v-if="!nuxt">
        <a @click="handleRoute(getUrl)" menuitem :class="{ 'active-item': isActive, 'active': state }" :style="{ fill: item?.fill }"
            v-if="!item?.action">
            <box-icon class="icon" :name="item?.icon"></box-icon>
            <p>{{ item?.label }}</p>
        </a>
        <a v-else :class="{ 'active-item': isActive }" :style="{ fill: item?.fill }" menuitem @click="Action(item)">
            <box-icon class="icon" :name="item?.icon"></box-icon>
            <p>{{ item?.label }}</p>
        </a>
    </div>
    <div v-else>
        <NuxtLink :to="getUrl" menuitem :class="{ 'active-item': isActive, 'active': state }"
            :style="{ fill: item?.fill }" v-if="!item?.action">
            <box-icon class="icon" :name="item?.icon"></box-icon>
            <p>{{ item?.label }}</p>
        </NuxtLink>
        <a v-else :class="{ 'active-item': isActive }" :style="{ fill: item?.fill }" menuitem @click="Action(item)">
            <box-icon class="icon" :name="item?.icon"></box-icon>
            <p>{{ item?.label }}</p>
        </a>
    </div>
</template>

<script setup>
import { defineProps, defineEmits, computed, ref, onMounted } from "vue";
const props = defineProps(["item", "parent", "nuxt"])
const emit = defineEmits(["action"]);

const handleRoute = (link) => {
    emit("action", link);
}

const isActive = computed(() => {
    if (props.parent) {
        console.log(`${props.parent?.url}${props.item?.url}`);
        return `${props.parent?.url}${props.item?.url}` === location?.href;
    } else {
        return `${props.item?.url}` === location?.href;
    }
})

const getUrl = computed(() => {
    if (props.parent) {
        return `${props.parent?.url}${props.item?.url}`;
    } else {
        return `${props.item?.url}`;
    }
});

</script>

<script>
export default {
    data() {
        return {
            state: false,
        }
    },
    methods: {
        Action(item) {
            this.$emit(item?.action, item);
            this.state = true;
        },
    }
};
</script>

<style scoped lang="scss">
a {
    display: flex;
    width: 300px;
    height: 50px;
    align-items: center;
    padding: 0 18px;
    text-decoration: none;

    color: var(--sidebar-color);

    &>i {
        transform: scale(1.5);
    }

    &>p {
        margin-left: 2em;
        margin-bottom: 0;
    }
}

.active {
    background: var(--primary);
}

p::first-letter {
    text-transform: uppercase;
}

a:hover {
    fill: white !important;
}

a:hover .sidebar-item-label {
    opacity: 100%;
    transform: translateX(32px);
}

.sidebar-item-label {
    padding: 0.2em 1em;
    position: absolute;
    transform: translateX(32px);
    transform: translateX(-200%);

    color: var(--sidebar-color);
    background: var(--primary);
    border-top-right-radius: 7px;
    border-bottom-right-radius: 7px;
    opacity: 0;
    transition: 0.25s;
}

@media screen and (max-width: 500px) {
    .sidebar-item-label {
        display: none;
    }
}
</style>