<script setup>
import { ref, onMounted, watch } from 'vue';
import "x-data-spreadsheet/dist/xspreadsheet.css";
import XSpreadsheet from "x-data-spreadsheet";
import ExportXLSX from '@/composables/ExportXLSX'

const props = defineProps({
  data: {
    type: Object,
    default: () => ({})
  },
  options: {
    type: Object,
    default: () => ({})
  },
  height: {
    type: String,
    default: "100%"
  },
  width: {
    type: String,
    default: "100%"
  }
});

const sheetEl = ref(null);
const sheetRef = ref(null);
const state = ref(props.data || {});
let sheet = ref(null);

onMounted(() => {
  const element = sheetEl.value;
  sheet.value = new XSpreadsheet(element, {
    view: {
      height: () => (element && element.clientHeight) || document.documentElement.clientHeight,
      width: () => (element && element.clientWidth) || document.documentElement.clientWidth
    },
    ...props.options
  })
    .loadData(state.value) // load data
    .change((data) => {
      state.value = data;
    });

  sheetRef.value = sheet.value;
});
</script>
<template>
  <!-- <button @click="ExportXLSX(sheetRef)">Export</button> -->
  <div :style="{ height: height || '100%', width: width || '100%' }" id="x-spreadsheet" ref="sheetEl"></div>
  <!-- {{ state }} -->
</template>