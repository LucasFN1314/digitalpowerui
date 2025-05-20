<template>
  <div id="table-container" flex flex-column flex-center>
    <div id="table" radius-border>
      <table class="table">
        <thead>
        <tr>
          <th
              class="text-center"
              scope="col"
              v-for="(head, key) in headers"
              noselect

              @click="Order(head?.toLowerCase(), true)"
          >
            {{ head }}
          </th>
        </tr>
        </thead>
        <tbody>
        <tr
            v-for="(element, key) in order_data"
            :key
            @contextmenu.prevent="emits('rightClick', element)"
            @click="
              () => {
                emits('action', element);
              }
            "
        >
          <td
              noelect
              v-for="(head, key2) in headers"
              :key="key2"
              class="text-center"
          >
            <div
                v-if="element?.[head?.toLowerCase()]?.html"
                v-html="element?.[head?.toLowerCase()]?.html"
                flex
                flex-center
            ></div>
            <div class="datacell" v-else flex flex-center>
                <span v-if="length">
                {{ limit(element?.[head?.toLowerCase()], length) }}
                </span>
              <span v-else>
                {{ element?.[head?.toLowerCase()]?.toLocaleString('es-ES') }}
              </span>
            </div>
          </td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script setup>
import {onMounted, ref, watch} from "vue";

const props = defineProps(["headers", "data", "length"]);
const emits = defineEmits(["action", 'rightClick']);

const order = ref(1);
const order_column = ref(null);
const order_data = ref([]);

onMounted(async () => {
  setTimeout(() => {
    Order();
  }, 500)
})

function Order(column, clicked = false) {
  if (clicked) order.value = -order.value;
  if (column !== order_column.value) {
    order.value = 1;
  }

  order_column.value = column;
  OrderData(props.data);

}

function OrderData(newValue) {
  if (!newValue) return;
  order_data.value = [...newValue].sort((a, b) => {
    const valA = isNaN(a?.[order_column.value]) ? a?.[order_column.value] : Number(a?.[order_column.value]);
    const valB = isNaN(b?.[order_column.value]) ? b?.[order_column.value] : Number(b?.[order_column.value]);

    return valA > valB ? order.value : valA < valB ? -order.value : 0;
  });
}



function limit(text, length) {
  if (text?.length > length) {
    return text.substring(0, length) + "...";
  }
  return text;
}

watch(
    () => props.data,
    (newValue, oldValue) => {
      if (newValue === oldValue) return;
      OrderData(newValue);
    },
    {deep: true}
);
</script>

<style scoped lang="scss">
#table {
  width: 100%;
  height: 60vh;
  overflow-y: auto;
  overflow-x: auto;

  box-shadow: 0px 0px 10px 1px rgba(0, 0, 0, 0.1);
}

#table-container {
  width: 90%;
  height: 60vh;
  margin-bottom: 1em;

  justify-content: start;
  padding-top: 1em;
}

th {
}

tr {
  cursor: pointer;
}

td {
  text-wrap: nowrap;
  vertical-align: middle;
  transition: var(--duration);

  &:hover {
    background: var(--primary);
    color: white;
  }
}

table {
  padding: 0;
  margin: 0;
}

thead {
  position: sticky;
  top: 0;
}

.red {
  background: var(--red);
  color: white;
}

.ingreso {
  /*  background: #70bf70;
    color: white;*/
}

.gasto {
  background: lightgray;
}
</style>
