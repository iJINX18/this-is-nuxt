<template>

<form  @submit.prevent="submitForm">
  <slot name = "header"/>
   <h3> {{recordCount}} </h3>
  <p>Task Name:  
      <input  v-focus v-model="form.task" placeholder="Anything to do?" required /> 
    </p>

    <p>Description: 
      <input v-model="form.description" placeholder="Enter description" required /> 
    </p>

    <p>Due Date: 
      <input v-model="form.dueDate" type="date" required /> 
    </p>

    <p>Choose Status: 
      <select v-model="form.status" required>
        <option disabled value="">Select status</option>
        <option value="To do">To do</option>
        <option value="On going">On going</option>
        <option value="Completed">Completed</option>
      </select>
    </p>  
    
    <button type="submit">Submit Task</button>
    <slot/>
    <p>{{ message }}</p>
</form>

</template>

<script setup>

 const vFocus = {
  mounted(el) {
    el.focus()
  }
}

const form =  reactive({
    task: '',
    description: '',
    dueDate: '',
    status: ''
})

const props = defineProps({
  recordCount: String
})

const emit = defineEmits(['submit-form'])

const submitForm = () => {
  emit('submit-form',form)
  reset ()
}

const reset = () =>{
form.task =''
form.description =''
form.dueDate =''
form.status =''
}



</script>

<style scoped>

button{
    background-color: goldenrod;
   
} 



.changeFormColor1{
  background-color: red;
  
}

</style>