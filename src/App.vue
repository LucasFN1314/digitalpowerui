<script setup>
import { ref } from "vue";
import { Documentation, Container } from "vuedigitalpowerui";

</script>

<template>
  <Documentation />
</template>

<style>
code {
  padding: 1em;
  display: block;
  background: rgb(238, 238, 238);
  color: black !important;
}

pre {
  background: transparent;
}

a {
  text-decoration: none !important;
}

#carousel {
  height: 200px;
}

.carimg {
  height: 100%;
}

.gridd {
  background: var(--primary);
  padding: 1em;
}

.sidebarD {
  height: 300px;
}
</style>
