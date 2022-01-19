<template>
    <div class="reminder">
        <div class="name"><span class="circle-span"></span>{{ task.name }}</div>
        <div class="date">Date: {{ task.date }}</div>
    </div>
</template>

<script>
export default {
    name: "Reminder",
    props: ['title', 'task'],
}
</script>

<style>
.reminder{
    border: 2px solid grey;
    border-radius: 5px;
    word-break: break-all;
    box-sizing: border-box;
    padding: 20px 10px;
    /* display: grid;
    grid-template-columns: repeat(auto-fit, minmax(10%, 1fr)); */
}
.name{
    display: flex;
    box-sizing: border-box;
    align-items: center;
    margin-left: 20px;
    flex-wrap: wrap;
}
.date{
    display: flex;
    margin-left: 40px;
}
/* .tag{
   
} */
/* .name{
   
} */
.circle-span{
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background: black;
  display: block;
  margin-right: 10px;
}
</style>