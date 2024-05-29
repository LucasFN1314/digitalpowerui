<template>
    <nav :id :class="{
        'open': menuState,
        'close': menuState === false,
        'closed': menuState === null,
        'fixedSidebar': fixed
    }" :style="{
        background: background
    }">
        <ul>
            <li>
                <a href="javascript:void(0)" @click="setMenu">
                    <box-icon class="icon" name="menu"></box-icon>
                </a>
            </li>
            <li v-for="(item, index) in items" :key="index">
                <SidebarItem v-if="!item?.group" :item="item" />
                <ul v-else groupitem>
                    <li nopointer grouplabel>
                        <a href="" :style="{ fill: item?.fill }">
                            <box-icon class="icon" :name="item?.icon"></box-icon>
                            <p>{{ item?.group }}</p>
                        </a>
                    </li>
                    <li v-for="(subitem, index) in item?.items" :key="index">
                        <SidebarItem :item="subitem" :parent="item" />
                    </li>
                </ul>
            </li>
        </ul>
    </nav>
</template>

<script setup>
import { ref, defineProps, onBeforeMount, onMounted } from "vue";
import SidebarItem from "./SidebarItem.vue";

const props = defineProps(["items", "id", "class", "background"]);

const Menu = ref([]);
const menuState = ref(null);

const setMenu = () => {
    menuState.value = (!menuState.value);
};

onBeforeMount(() => {
    window.removeEventListener("click", clickOutsideHandler);
});
onMounted(() => {
    setTimeout(() => {
        window.addEventListener("click", clickOutsideHandler);
    }, 300)
});

const clickOutsideHandler = () => {
    var elem = document.getElementById(props.id);
    if (
        elem?.id !== (`#${props.id}`) &&
        !elem.contains(event.target) && menuState.value === true
    ) {
        menuState.value = false;
    }
};

</script>

<style scoped>
nav {
    overflow-y: auto;
    overflow-x: hidden;
    width: 62px;
    height: 100%;
}

ul {
    list-style: none;
    padding: 0;
    margin: 0;
}

li {}

a {
    display: flex;
    width: 300px;
    height: 50px;
    align-items: center;
    padding: 0 18px;
    text-decoration: none;

    color: var(--sidebar-color);
}

i {
    transform: scale(1.5);
}

p {
    margin-left: 2em;
    margin-bottom: 0;
}

.fixedSidebar {
    position: fixed;
    top: 0;
    left: 0;
    z-index: 100;
    height: 100%;
}

.open {
    width: 300px;
    animation: open;
    animation-duration: var(--duration);
}

.close {
    width: 62px;
    animation: close;
    animation-duration: var(--duration);
}

@keyframes open {
    0% {
        width: 62px;
    }

    100% {
        width: 300px;
    }
}

@keyframes close {
    0% {
        width: 300px;
    }

    100% {
        width: 62px;
    }
}
</style>