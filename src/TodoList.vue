<template>
  <div class="todo-container">
    <h1>Ma Todo List</h1>
    
    <form @submit.prevent="addTask" class="task-form">
      <input type="text" placeholder="Ajouter une tâche" v-model="newTask" class="task-input">
      <button :disabled="newTask==''" class="add-button">Ajouter une tâche</button>
    </form>

    <table class="task-table">
      <thead>
        <tr>
          <th>Title</th>
          <th>Date</th>
          <th>Complete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="task in sort" :key="task.title">
          <td :style="{ 'text-decoration': task.complete ? 'line-through' : 'none' }">{{ task.title }}</td>
          <td>{{ task.date }}</td>
          <td>
            <input type="checkbox" v-model="task.complete" @change="sort" class="checkbox">
          </td>
        </tr>
      </tbody>
    </table>
<div>
<label for="">Masquer les taches completées</label>
<input type="checkbox" v-model="hiddenTasks" @change="hidden">
</div>
    <p v-if="tasks.length === 0">Aucune tâche pour l'instant</p>
  </div>
</template>


<script setup>
import { ref , computed } from 'vue'
const newTask = ref('')
const hiddenTasks = ref(false)
const tasks = ref([
  { title: 'Faire les courses', complete: false, date: '2021-10-01' },
  { title: 'Faire le ménage', complete: true, date: '2021-10-02' },
  { title: 'Faire du sport', complete: false, date: '2021-10-03' },
  { title: 'Faire la cuisine', complete: true, date: '2021-10-04' },
  { title: 'Faire la vaisselle', complete: false, date: '2021-10-05' },
])
const addTask = (e) => {
  e.preventDefault();
  // alert(newTask.value);
  
  tasks.value.push({ title: newTask.value, complete: false, date: new Date().toISOString().split('T')[0] })
  newTask.value = ''
}

// /coompited pour optimiser les performance: ca ne charge que lorsque il uaya changement des variable concerné
const sort =computed(() => {
  console.log('demo');
  
  //trier par date
  // const sortDate = tasks.value.sort((a, b) => {
  //   return new Date(a.date) - new Date(b.date);
  // });

  //trier par complete

  
   const sortTask = tasks.value.toSorted((a, b) => {
    return (a.complete > b.complete ?  1 : -1);
  });

  if(hiddenTasks.value){

   return  sortTask.filter(t =>t.complete==false)
  }
  return sortTask
});

console.log(sort.value);
console.log(sort.value);
console.log(sort.value);



const hidden= () => {

  if(hiddenTasks.value){

   return  tasks.value.filter(t =>t.complete==false)
  }
  return tasks.value
}

</script>


<style scoped>
.todo-container {
  max-width: 600px;
  margin: auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 2px 2px 12px rgba(0, 0, 0, 0.1);
  background-color: #f9f9f9;
}

h1 {
  text-align: center;
  color: #333;
}

.task-form {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
}

.task-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 16px;
}

.add-button {
  padding: 10px 15px;
  background-color: #5cb85c;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-button:hover {
  background-color: #4cae4c;
}

.task-table {
  width: 100%;
  border-collapse: collapse;
}

.task-table th, .task-table td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: left;
}

.task-table th {
  background-color: #f2f2f2;
  color: #333;
}

.checkbox {
  cursor: pointer;
}

p {
  text-align: center;
  color: #777;
}
</style>