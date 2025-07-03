<template >
  <div v-bind="noColor">
    <span>Filter Status: </span>
    <select v-model="selectedStatus" >
      <option value="All">All</option>
      <option value="To do">To do</option>
      <option value="On going">On going</option>
      <option value="Completed">Completed</option>
    </select>
  </div>
</template>

<script setup>
import { defineEmits, ref, useAttrs, watch } from 'vue';

const emit = defineEmits(['filter-status']);
const selectedStatus = ref('All');
const noColor = useAttrs()

watch(selectedStatus, (newStatus) => {
  emit('filter-status', newStatus);
});
</script>

<style scoped>  

.removeColor {
  background-color:burlywood;
  color: black;
  width: 265px;
  text-align: center;
}
</style>
