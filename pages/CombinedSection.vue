<template>
  <div class="container">

    <!-- School  -->
    <div class="section">
      <h3>School</h3>
      <div class="button-group">
        <button 
          v-for="s in sortedSchools" 
          :key="s.name" 
          @click="selectSchool(s.name)"
          :class="{ active: selectedSchool === s.name }">
          {{ s.name }}
        </button>
      </div>
    </div>

    <!-- Add Category Form -->
    <div class="section" v-if="selectedSchool">
      <h3>Add Category</h3>
      <form @submit.prevent="addCategory">
        <label>Category Name:</label>
        <input v-model="newCategory.name" type="text" required />

        <label>Category ID:</label>
        <input v-model="newCategory.id" type="text" required />

        <label>Sequence:</label>
        <input v-model.number="newCategory.sequence" type="number" min="0" required />

        <button type="submit">Add Category</button>
      </form>
    </div>

    <!-- Category Selection -->
    <div class="section" v-if="selectedSchool">
      <h3>Category</h3>
      <div class="button-group">
        <button 
          v-for="c in sortedFilteredCategories" 
          :key="c.id"
          @click="selectCategory(c)"
          :class="{ active: selectedCategory?.id === c.id }">
          {{ c.name }}
        </button>
      </div>
    </div>

    <!-- Add Class Form -->
    <div class="section" v-if="selectedCategory">
      <h3>Add Class</h3>
      <form @submit.prevent="addClass">
        <label>Class Name:</label>
        <input v-model="newClass.name" type="text" required />

        <label>Grade:</label>
        <input v-model="newClass.grade" type="text" required />

        <button type="submit">Add Class</button>
      </form>
    </div>

    <!-- Class List Table -->
    <div class="section" v-if="selectedCategory">
      <h3>Class List</h3>
      <table v-if="classList.length">
        <thead>
          <tr>
            <th>Name</th>
            <th>Grade</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="cls in classList" :key="cls.name">
            <td>{{ cls.name }}</td>
            <td>{{ cls.grade }}</td>
          </tr>
        </tbody>
      </table>
      <p v-else>No class data available.</p>
    </div>

  </div>
</template>

<script setup>
import { ref, reactive, computed, onMounted } from 'vue'

const data = reactive({
  school: [
    { name: 'Malaysia', sequence: 1 },
    { name: 'Thailand', sequence: 2 },
    { name: 'Philippines', sequence: 3 }
  ],
  category: [],
  class: {}
})

const selectedSchool = ref('')
const selectedCategory = ref( )

const newCategory = reactive({
  name: '',
  id: '',
  sequence: 0
})

const newClass = reactive({
  name: '',
  grade: ''
})

const sortedSchools = computed(() => {
  return [...data.school].sort((a, b) => a.sequence - b.sequence)
})

const sortedFilteredCategories = computed(() => {
  if (!selectedSchool.value) return []
  return data.category
    .filter(c => c.school === selectedSchool.value)
    .sort((a, b) => a.sequence - b.sequence)
})

const classList = computed(() => {
  if (!selectedCategory.value) return []
  return data.class[selectedCategory.value.id] || []
})

const selectSchool = (schoolName) => {
  selectedSchool.value = schoolName
  selectedCategory.value = null
}

const selectCategory = (category) => {
  selectedCategory.value = category
}

const addCategory = () => {
  if (!newCategory.name || !newCategory.id || newCategory.sequence === null) {
    alert("Please fill in all category fields.")
    return
  }
  data.category.push({
    name: newCategory.name,
    id: newCategory.id,
    school: selectedSchool.value,
    sequence: newCategory.sequence
  })
  Object.assign(newCategory, { name: '', id: '', sequence: 0 })
  saveData()
}

const addClass = () => {
  if (!newClass.name || !newClass.grade) {
    alert("Please fill in all class fields.")
    return
  }
  const catId = selectedCategory.value.id
  if (!data.class[catId]) {
    data.class[catId] = []
  }
  data.class[catId].push({
    name: newClass.name,
    grade: newClass.grade
  })
  Object.assign(newClass, { name: '', grade: '' })
  saveData()
}

onMounted(() => {
  const stored = localStorage.getItem('schoolData')
  if (stored) {
    const parsed = JSON.parse(stored)
    data.category = parsed.category || []
    data.class = parsed.class || {}
  }
})

const saveData = () => {
  localStorage.setItem('schoolData', JSON.stringify({
    category: data.category,
    class: data.class
  }))
}

</script>

<style scoped>
.container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  padding: 16px;
}

.section {
  flex: 1 1 250px;
  border: 1px solid #ccc;
  padding: 12px;
  border-radius: 4px;
}

h3 {
  margin-bottom: 8px;
  text-align: center;
}

.button-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-top: 8px;
}

button {
  padding: 6px 12px;
  border: 1px solid #ccc;
  background: #eee;
  cursor: pointer;
  border-radius: 4px;
  transition: background 0.3s;
}

button:hover {
  background: #ddd;
}

button.active {
  background: red;
  color: white;
  border-color: red;
}

input {
  width: 100%;
  padding: 6px;
  margin-top: 4px;
  margin-bottom: 8px;
  box-sizing: border-box;
}

table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 8px;
}

th, td {
  border: 1px solid #ccc;
  padding: 6px;
  text-align: left;
}

p {
  margin-top: 8px;
  color: gray;
}
</style>
