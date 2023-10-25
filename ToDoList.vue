<template>
  <div class="header">
    <h1>My To-Do List</h1>

    <input type="text" class="new-task" v-model="newTask" placeholder="Enter your task" />
    <button class="add-task" @click="addTask">Add</button>
    <div class ="box">
    <ol>
      
      <li v-for="task in filteredTasks" :key="task.id">
        <input type="checkbox" v-model="task.completed">
        <input type="text" v-model="task.description" v-if="task.editing">
        <span v-else>{{ task.description }}</span>
        <br>
        <button class="edit-task" @click="editTask(task)">Edit</button>
        <button class="update-task" @click="updateTask(task)">Update & Save</button>
        <button class="delete-task" @click="removeTask(task)">Delete</button>
      </li>
    </ol>
    </div>
    <br>
    <br>
    <div class="custom-select">
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="active">Active</option>
    </select>
  </div>
  </div>
</template>

<script>
export default {
  name: 'ToDoList',

  data() {
    return {
      newTask: '',
      tasks: [],
      filter: 'active',
    };
  },

  computed: {
    filteredTasks() {
      if (this.filter === 'all') {
        return this.tasks;
      }

      return this.tasks.filter(task => task.completed === (this.filter === 'completed'));
    },
  },

  methods: {
    addTask() {
      if (this.newTask) {
        this.tasks.push({
          id: Math.random().toString(36).substring(7),
          description: this.newTask,
          completed: false,
          editing: false,
        });

        this.newTask = '';
      }
    },

    editTask(task) {
      task.editing = true;
    },

    updateTask(task) {
      // Save the edited task
      task.editing = false;
    },

    removeTask(task) {
      this.tasks = this.tasks.filter(t => t !== task);
    },
  },
};
</script>

<style>
.task-list {
  list-style: none;
  margin: 0;
  padding: 0;
}

.task-item {
  display: flex;
  align-items: center;
  padding: 20px;
}

.task-item input[type="checkbox"] {
  margin-right: 10px;
}

.task-item input[type="text"] {
  flex: 1;
  border: 1px solid #ccc;
  padding: 5px;
}

.task-item button {
  margin-left: 10px;
}

.new-task,.add-task{
  display: block;
  width: 100%;
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 10px;
  font-style: normal;
  gap: 30px; 
  
}
.custom-select {
  position: relative;
  font-family: Arial;
}


.header{
  padding: 1rem;
    background-color: rgb(232, 197, 197);
    text-align: center;
    width: 40%;
    top: 50%;
    left: 50%;
    font-family: Georgia,Serif;
    min-width: 600px;
    position: absolute;
    min-height: 300px;
    transform: translate(-50%,-50%);
    border-style: solid;
    border-width: 2px;
    
}

.update-task{
  background-color: white;
  color: black;
  border: 2px solid #4CAF50; /* Green */
  padding: 5px 5px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.edit-task{
  background-color: white; 
  color: black; 
  border: 2px solid #008CBA;
  padding: 5px 5px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}
.delete-task{
  background-color: white; 
  color: black; 
  border: 2px solid #f44336;
  padding: 5px 5px;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

</style>