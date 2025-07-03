<template>


    <TaskForm :class = "[{
      meetsTwo: data.length >2,
      meetsThree: data.length>3, }]"
      :record-count = "recordCount"
      @submit-form="submitForm"
      >
        <template #header >
          <NuxtLink to="/" class="nuxt-link">< Back</NuxtLink>
          <p><b>TASK TRACKER</b></p>
        </template>
        
    <TaskFilter
        @filter-status = "filterTasks" 
        class = "removeColor" />
    </TaskForm>

    <TaskStatus
    :data ="filteredData" 
    :all-data = "data"
    :show-data = "showData"
    @toggle-data = "toggleData"
    @remove-item = "removeItem"
    />  

    <TaskSummary
    :status-summary = "statusSummary"/>

</template>


<script setup>
import TaskForm from '../components/TaskComps/TaskForm.vue'
import TaskStatus from '../components/TaskComps/TaskStatus.vue'
import TaskFilter from '../components/TaskComps/TaskFilter.vue'
import TaskSummary from '../components/TaskComps/TaskSummary.vue'
import { ref, computed, watch, onMounted, provide } from 'vue'


const data = ref ([])
const filteredData = ref([])   
const showData = ref(false)
const selectedStatus = ref('All')

let conStruct = data.value.constructor

provide ('message', filteredData.value)
provide ('message', data.value)

 onMounted(() => {
  const dataSaved = localStorage.getItem('task-data')
   if (dataSaved) {
     data.value = JSON.parse(dataSaved)
   }
    filteredData.value = data.value
 })

 watch(data, (newVal) => {
   localStorage.setItem('task-data', JSON.stringify(newVal))
 }, { deep: true })

 watch([data, selectedStatus], () => {
  filteredData.value = selectedStatus.value === 'All'
    ? data.value
    : data.value.filter(item => item.status === selectedStatus.value)
}, { deep: true })

const submitForm = (value) => {
  data.value.push({
        task : value.task,
        desc : value.description,
        date : value.dueDate,
        status : value.status
    })

    data.value.sort((a, b) => new Date(a.date) - new Date(b.date))
    
} 

const recordCount = computed (() => {
  return data.value.length <= 5 ? 'Record is Less than or Equal to 5' : 'Record is More than 5'
})

const filterTasks = (status) => {
  if (status === 'All' ){
    filteredData.value = data.value
  }
 else {
     filteredData.value = data.value.filter(item => item.status === status)
  
  }
}

const removeItem = (index) => {
  data.value.splice(index, 1)
}


const toggleData = () => {
  showData.value = !showData.value
}

const becomesRed = computed (() => {
  data.value.length > 2
})

const statusSummary = computed(() => {
  return data.value.reduce((acc, task) => {
    acc[task.status] = (acc[task.status] || 0) + 1;
    return acc;
  }, {
  });
});


</script>




<style scoped>

.meetsTwo {
  background-color: red;
  text-align: left;
  color: azure;

}


.meetsThree {
  background-color: red;
  text-align: center;
  color: azure;

}
.changeFormColor{
  background-color: aquamarine;
  text-align: center;

}

</style>