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
              <li v-for="(task) in tasks" :key="task.id">
                <div class="action-icons">
                  <p v-bind:id="task.id">Edit</p>
                  <p v-bind:id="task.id" @click="delete_task">Delete</p>
                </div>
                <p>Task name: {{task.name}}</p>
                <p>Descrpition: {{task.description}}</p>
              </li>
            </div>
          </ul> 
      </div>

    </div> 

    <div class="right">
      <div class="right-container">
        <div class = "reminders">
          <h3>Reminders</h3>
          <ul>
            <div class="reminders-list">
              <li v-for="(reminder, index) in reminders" :key="index">
                <p><span class="circle-span"></span>{{reminder.name}}</p>
              </li>
            </div>
          </ul> 
      </div>
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
          {id:'1', name: "Report", description: "Daily Report"},
          {id:'2', name: "Meeting", description: "Afternoon Discussion"},
      ],
      reminders: [
        { id:'1', name: "Meeting", description: "Afternoon Discussion"},
      ]
    }
},
methods: {
    add(e){
      e.preventDefault();
      this.tasks.push({name: this.task_name, description: this.task_description})
      alert('Task \'' + this.name + '\' Added!')
    },
    delete_task(e){
      // if(confirm("Are You sure")){}s
      console.log(e.target.id)
      // this.tasks = this.tasks.filter(t => t.id == e.id)
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
.center, .right{
  width: 100%;
  border: 2px solid grey;
  border-radius: 5px;
  padding: 20px 10px;
  box-sizing: border-box;
}
.center{
  grid-column: 1;
}

.right{
  grid-column: 2;
}

.hello{
  padding: 20px;
  box-sizing: border-box;
  display: grid;
  grid-template-columns: repeat(2, minmax(300px, 1fr));
  grid-gap: 10px;
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
    position: relative;
}
.action-icons{
  position: absolute;
  top: 0;
  right: 0;
  display: flex;
  color: greenyellow;
}

.action-icons >p {
  padding: 0 5px;
  cursor: pointer;
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
.reminders-list > li > p{
  display: flex;
  align-items: center;
}
.reminders-list > li{
    width: 100%;
    justify-content: flex-start;
    display: flex;
    box-sizing: border-box;
    padding-left: 15%;
}
.circle-span{
  width: 5px;
  height: 5px;
  border-radius: 50%;
  background: black;
  display: block;
  margin-right: 10px;
}
</style>
