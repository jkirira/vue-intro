
<template>
  <div id="app">
    
    <div class="header">
      <h1>Vue components</h1>
    </div>

    <div class="container">
        
        <div class="right">
           <h3>Reminders</h3>
           <reminder v-for="(task, index) in toRemind" :key="index" v-bind:task="task"></reminder>
           <!-- <reminder title="reminder"></reminder> -->
        </div>

        <div class="center">
        
        <div class="tasks-div">
          <h3>Saved Tasks</h3>
          <task v-for="(task, index) in tasks" :key="index" v-bind:task="task" @setReminder="remind" @forgetReminder="dontRemind" >

            <template v-slot:task-name>
              {{task.name}}
            </template>

            <template v-slot:task-description>
              {{task.description}}
            </template>

          </task>
        </div>
        <div class="add-task-div">
          <h3>Add a Task</h3>

          <task-form @add_task="add"></task-form>
          
        </div>
          
        </div>
    </div>

  </div>
</template>

<script>
import Task from './components/Task.vue'
import TaskForm from './components/TaskForm.vue'
import Reminder from './components/Reminder.vue'

export default {
  name: 'App',
  components: {
    Task,
    TaskForm,
    Reminder
  },
  data(){
    return {
      welcome_message: "Tasks",
      rawHTML: `<h5>Enter a task</h5>`,
      checked:[],
      description_disabled: true,
      if_toggle: true,
      show_toggle: true,
      tasks: [
        {id:'1', name: "Report", description: "Daily Report", date: "29-01-2020", remind_me: true},
        {id:'2', name: "Meeting", description: "Afternoon Discussion", date: "29-01-2020", remind_me:false},
      ]
    }
  },
  computed: {
    toRemind(){
      return this.tasks.filter((task) => task.remind_me == true)
    }
  },
  methods: {
    toggle_show: function(){
      this.show_toggle = !this.show_toggle
    },
    add(task_data){
      console.log(task_data)
      this.tasks.unshift({id: this.tasks.length+1, name: task_data.name, description: task_data.description, date: task_data.date, remind_me: task_data.remind_me})
      console.log(this.tasks)
      alert('Task \'' + task_data.name + '\' Added!')
    },
    remind(target_id){
      let t = this.tasks.find(task => task.id == target_id)
      t['remind_me'] = true
      console.log(t)
    },
    dontRemind(target_id){
      let t = this.tasks.find(task => task.id == target_id)
      t['remind_me'] = false
      console.log(t)
    },
  }

}
</script>

<style>
html, body{
    font-size: 16px;
    margin: 0;
    padding: 0;
    height: 100%;
    overflow-y: scroll;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 100%;
}
.header{
  background: #34495E;
  color: white;
  height:10%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.container{
  box-sizing: border-box;
  grid-gap: 20px;
  padding: 10px;
  font-size: 1.4rem;
}
.center, .right{
  width: 100%;

  border-radius: 5px;
  padding: 20px 10px;
  box-sizing: border-box;

}
.center{
  grid-column: 2;

  box-sizing: border-box;
}
.add-task-div{
  grid-row: 1;
  /* border: 2px solid grey; */
}
.tasks-div{
  grid-row: 2;
  /* border: 2px solid grey; */
  margin-bottom: 20px;

}
.right{
  grid-column: 1;
}

@media screen and (min-width: 350px) {
  .container{
    font-size: 1.5rem;  
  }
    
}

@media screen and (min-width: 750px){
  .container{
    font-size: 2rem;
    box-sizing: border-box;
    padding: 0px 10%;
  }
  .task, form{
    padding: 25px;
  }
}

@media screen and (min-width: 1024px){
  .container{
    font-size: 2rem;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    box-sizing: border-box;
    padding: 0px 10%;
  }
  button{
    font-size: 1.4rem;
  }
}
</style>
