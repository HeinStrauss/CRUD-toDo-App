<template>
  <h1>To do list</h1>
    <form @submit.prevent="addNewToDo">
      <label>To Do:</label>
      <input  type="text" v-model="newToDo"/>
      <button>Add New ToDo</button>
    </form>
<br>
  <h1>To pack list</h1>
    <form>
  <label>To Pack:</label>
  <input  type="text" v-model="newToPack"/>
  <button @click.prevent="addNewToPack(newToPack)">Pack new item</button>
    </form>
    <div v-for="(todo, index) in toDoList" :key="index">
      <h3 :class="{done: todo.done}" @click="toggleDone(todo)">{{todo.content}}</h3>
      <button @click="deleteTodo(todo, index)">Delete</button>
    </div>
<br>
  <button @click="markAllDone">Mark All Done</button>
  <button @click="unmarkAll">Unmark All </button>
<br>
  <button @click="deleteAll">Delete All The Above</button>
</template>

<script>
import { ref } from 'vue';
export default {
  name: 'App',
  setup(){
    //variables
    const newToPack = []
    const newToDo = ref('');
    const toDoList = ref([]);
    //functions
    function addNewToPack(item){
      console.log('You need to pack in ' + item)
    }
    function addNewToDo() {
      console.log('You need to ' + newToDo.value );
      toDoList.value.push({
        done:false,
        content: newToDo.value,
      });
      newToDo.value="";
    }
   function toggleDone(todo){
     todo.done = !todo.done
   }
   function deleteTodo(todo, index){
     toDoList.value.splice(index, 1);
     console.log("you deleted an item");
   }
   function markAllDone(){
     toDoList.value.forEach ((todo) => todo.done=true);
   }
   function unmarkAll(){
     toDoList.value.forEach ((todo) => todo.done=false);
   }
   function deleteAll(){
     toDoList.value = [];
   }
    //returns
    return {
      unmarkAll,
      deleteAll,
      markAllDone,
      deleteTodo,
      toggleDone,
      addNewToPack,
      addNewToDo,
      newToDo,
      toDoList,
      newToPack,
    };
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.done{
  text-decoration: line-through;
}
</style>
