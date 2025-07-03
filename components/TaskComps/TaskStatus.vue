<template>
<div>
      <!-- <div>{{ data }}</div>
      <div>{{ props.data }}</div>  -->
      <table>
        <thead>
        <tr>
          <th>ITEM</th>
          <th>DUE DATE</th>
          <th>TASK</th>
          <th>DESCRIPTION</th>
          <th>STATUS</th>
          <th>ACTION</th>
        </tr>
        </thead>
        <tbody>
          <tr v-for="(item, index) in props.data" :key="'filtered' + item.date + item.task">
            <td>{{index + 1}}</td>
            <td>{{item.date}}</td>
            <td>{{item.task}}</td>
            <td>{{item.desc}}</td>
            <td><select v-model="item.status" :class="changeColor(item)">
                <option value="To do">To do</option>               
                <option  value="On going">On going</option>
                <option  value="Completed">Completed</option>
            </select>

          </td>
            <button class ="removeBtn" @click="removeItem">Remove</button>
          </tr>
        </tbody>
     </table>   
       <button @click="toggleData">{{showData ? 'Hide': 'Show'}} Data</button>
  <Transition name="fadeTable"  >
  <table v-if = "showData" class="allDataTable">
      <thead>
        <tr>
          <th>ITEM</th>
          <th>DUE DATE</th>
          <th>TASK</th>
          <th>DESCRIPTION</th>
          <th>STATUS</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in props.allData" :key="'original' + item.date + item.task">
          <td>{{ index + 1 }}</td>
          <td>{{ item.date }}</td>
          <td>{{ item.task }}</td>
          <td>{{ item.desc }}</td>
          <td>{{ item.status }}</td>
        </tr>
      </tbody>
    </table>
  </Transition>
</div>
</template>

<script setup>

const props = defineProps({
    data: Array,
    allData: Array,
    showData: Boolean
})

const emit = defineEmits([
    'remove-item', 'toggle-data'
])

const removeItem = () => {
  emit('remove-item')
}

const toggleData = () => {
  emit('toggle-data')
}



const changeColor = (item) => {
    if (item.status == 'To do')
    return 'toDo'
    
    if (item.status == 'On going')
     return 'onGoing'
    
    if (item.status == 'Completed')   
     return 'gotCompleted' 
}

</script>

<style scoped>
.toDo{
    background-color: grey
}
.onGoing{
    background-color: yellow
}
.gotCompleted{
    background-color: green
}

.removeBtn{
  background-color: red;
  color: white;
  align-items: center;
  width: 100%;
  padding: 1px;
  border-radius: 2px; 
}

.fadeTable-enter-active,
.fadeTable-leave-active {
  transition: opacity 0.5s ease;
}

.fadeTable-enter-from,
.fadeTable-leave-to{
  opacity: 0;
}

.allDataTable{
  background-color: aqua;
}
option {
    background-color: #f6f7f9;
}

button{
  background-color: darkcyan;
}

</style>