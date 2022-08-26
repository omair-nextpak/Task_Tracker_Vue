<template>
  <div>
    <div class="logo-vue">
      <img alt="Vue logo" src="./assets/logo.png" />
    </div>
    <div class="container">
      
      
      <Header @toggle-addtask="toggleAddTask" title="Task Tracker" />
      <div v-show="showAddTask">
        <AddTask @add-task="addTask"/>
      </div>
      <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    </div>
  </div>
</template>


<script>
import Header from "./components/Header.vue";
import Tasks from "./components/Tasks.vue";
import AddTask from './components/AddTask'
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    };
  },
  methods: {
    addTask(newTask){
      this.tasks.push(newTask);
    },
    toggleAddTask(){
      this.showAddTask = !this.showAddTask;
    },
    deleteTask(id) {
      if (confirm("Are you sure you want to delete")) {
        console.log("APP", id);
        this.tasks = this.tasks.filter((t) => t.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks[this.tasks.findIndex(t => t.id == id)].reminder= !this.tasks[this.tasks.findIndex(t => t.id == id)].reminder;
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Doctos Appointment",
        day: "March 1st at 2:30pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Eat food",
        day: "March 2nd at 2:30pm",
        reminder: false,
      },
    ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
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
.logo-vue {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
