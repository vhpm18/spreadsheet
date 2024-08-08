<script setup>
import { ref, onMounted } from 'vue'
import Spreadsheet from "x-data-spreadsheet";


defineProps({ msg: String })
const xspreadsheet = ref(null)

onMounted(() => {
  const s = new Spreadsheet(xspreadsheet.value)
    .loadData({}) // load data
    .change(data => {
      // save data to db
    });

  s.validate()
})
</script>

<template>
  <div ref="xspreadsheet" id="xapp" />
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
