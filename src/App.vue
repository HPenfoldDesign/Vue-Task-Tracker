<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker - rebuild https://vuejs.org/guide/quick-start.html#with-build-tools" :addTaskbuttonChange="showAddTask" />
    <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    <!--delete-task has carried itself up to App.vue to fire off deleteTask function.-->
  </div>
</template>


<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
},
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
    },
    addTask(task) {
      this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if (confirm('Delete this Task?')) {
        this.tasks = this.tasks.filter((task) =>
        {
          return task.id!==id
          // returns all task id's apart from the one thats clicked. Component traversel is usually managed in Vuex for larger projects.
        }
      )
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => 
        task.id === id ? { ...task, reminder: !task.reminder } : task
      )
    },
  },
  created() { //this data would usually be brought in from a database.
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Appointment',
        day: 'June 1st at 14.30',
        reminder: true,
      },
       {
        id: 2,
        text: 'Shopping',
        day: 'June 4th at 9.00',
        reminder: false,
      },
       {
        id: 3,
        text: 'Cutting the lawn',
        day: 'June 9th at 17.00',
        reminder: false,
      },
    ]
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
