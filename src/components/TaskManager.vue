<script>
let id = 0
export default{
    data(){
        return{
            newTodo : '',
            newTodoDuration : 0,
            todos : [
                        {id: id++, done:true, text:"This is task!", duration:0},
                        {id: id++, done:false, text:"Looks like there is more??", duration:0},
                    ]
            }
    },
    methods : {
        addTodo(){
            console.log("Add!")
            this.todos.push({ id: id++, done:false, text: this.newTodo , duration:this.newTodoDuration})
            this.newTodo = ''
            this.newTodoDuration = 0
            console.log(this.todos)
        },
        removeTodo(todo){
            console.log("Remove!")
            this.todos = this.todos.filter((t) => t !== todo)
        }
    }
}
</script>

<template>
  <div class="TaskManager">
      <h1 class="taskManagerPlaceholder">Tasks</h1>
      <form @submit.prevent="addTodo">
            <input v-model="newTodo">
            <input type="number" v-model="newTodoDuration">
            <button>Add Task</button>    
        </form>
      <ul>
        <li class="listElem" v-for="todo in todos" :key="todo.id">
            {{todo.text}}
            <button v-on:click="removeTodo(todo)">X</button>
        </li>
       </ul>
  </div>
</template>

<style>
.taskManagerPlaceholder{
    color: white;
    text-align: center;
}
.listElem{
    color: white;
    text-align: center;
}
form
{
    display:flex;
    justify-content: center;
}

</style>
