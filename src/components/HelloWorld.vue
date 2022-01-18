<template>
  <div class="hello">
    <div class="center">
      <form>
        <div class="form-entry">
          {{ welcome_message }}
          <p v-html="rawHTML"></p>
        </div>

        <div class="form-entry">
          <div class="label-div">
            <label for="name">Task Name</label>
          </div>
          <div class="label-div">
            <input type="text" id="name" v-model="task_name">
          </div>
        </div>

        <div class="form-entry">
          <div class="label-div">
            <label for="description" :input='description_disabled = false'>Task Description</label>
          </div>
          <div class="label-div">
            <textarea id="description" v-model="task_description" v-bind:disabled="description_disabled"></textarea>
          </div>
        </div>

        <div class="form-entry">
          <div class="label-div">
            <input type="checkbox" id="reminder" v:model="remind_me" /><label for="reminder">Set Reminder</label>
          </div>
        </div>

        <div class="form-entry">
            <button v-on:click="add" >Add Task</button>
        </div>

      </form>
      
      <div class>
          <h3>Saved Tasks</h3>
          <ul>
            <div class="task-list">
              <li v-for="(task, index) in tasks" :key="index">
                <p>Task name: {{task.name}}</p>
                <p>Descrpition: {{task.description}}</p>
              </li>
            </div>
          </ul> 
      </div>

    </div> 
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      welcome_message: "Tasks",
      rawHTML: `<h5>Enter a task</h5>`,
      task_name: '',
      task_description: '',
      remind_me: '',
      description_disabled: true,
      tasks: [
          {name: "Report", description: "Daily Report"},
          {name: "Meeting", description: "Afternoon Discussion"},
      ],
      reminders: [
        { name: "Meeting", description: "Afternoon Discussion"},
      ]
    }
},
methods: {
    add(e){
      e.preventDefault();
      this.tasks.push({name: this.task_name, description: this.task_description})
      alert('Task \'' + this.name + '\' Added!')
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.center{
  margin: auto;
  width: 50%;
  border: 2px solid grey;
  border-radius: 5px;
  padding: 20px 10px;
  box-sizing: border-box;
}
.hello{
  padding: 30px;
  box-sizing: border-box;
  display: flex;
  justify-content: center;
}
.label-div{
  display: flex;
  justify-content: flex-start;
  width: 100%;
  padding-left: 35%;
  box-sizing: border-box;
  margin-bottom: 5px;
}
.task-list{
  display: flex;
  flex-direction:column;

}
.task-list >li{
    box-sizing: border-box;
    padding-left: 30%;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    display: flex;
      margin-bottom: 3px;
  border-bottom: 2px solid greenyellow;
}
.task-list > li >p{
  align-self: flex-start;
}
.form-entry{
  display: flex;
  align-items: center ;
  justify-content: center;
  flex-direction: column;
  margin-bottom: 5px;
}
</style>
