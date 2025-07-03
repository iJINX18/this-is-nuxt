<template> 
<form @submit.prevent = "onSubmit">
    <label>Enter name</label>
    <input v-model = "form.name" type = 'text' placeholder="name"/>
    <label>Enter ID</label>
    <input v-model = "form.id" type = 'text' placeholder="id"/>
    <label>Sequence</label>
    <input v-model = "form.seq" type = 'number'/>
    <button>Submit</button>
    <p>{{ arr }}</p>
    <p>{{ names }}</p>
</form>

<table>
    <thead>
        <td>Name</td>
        <td>ID</td>
        <td>Sequence</td>
    </thead>
    <tr v-for="data in arr">
        <td>{{ data.name }}</td>
        <td>{{ data.id }}</td>
        <td>{{ data.seq }}</td>
    </tr>
</table>
 <form @submit.prevent = "submitTask">
    <select v-model = "names" >
        <option v-for ="name in names">{{name}}</option>
    </select>
</form> 
</template>
<script setup>

const form = reactive({
    name: '',
    id: '',
    seq: 0
})

const arr = ref([])

const names = computed(() =>{
    return arr.value.map(items => items.name)
}) 



const onSubmit = () => {
    arr.value.push({name : form.name, id : form.id, seq : form.seq})
    console.log(arr.value)
    Object.assign(form, {
    name: '',
    id: '',
    seq: 0
})

localStorage.setItem('data-arr',JSON.stringify(arr.value))
}

onMounted(() =>{
const savedDate = localStorage.getItem('data-arr')
console.log('jjjjj',savedDate)
})

</script>
<style scoped>

</style>