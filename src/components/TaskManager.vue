<script>
export default {
  props: {
    todos: Array,
  },

  data() {
    return {
      newTodo: {
        text: 'New Todo',
        duration: 5,
        done: false,
      }
    }
  },
}
</script>

<template>
  <div class="TaskManager">
      <h1 class="taskManagerPlaceholder">Tasks</h1>
      <form @submit.prevent="this.$emit('addTodo', newTodo)">
        <input v-model="newTodo.text">
        <input type="number" v-model="newTodo.duration">
        <button>Add Task</button>    
      </form>
      <ul>
        <li class="listElem" v-for="todo in todos" :key="todo.id">
          <span @click="this.$emit('setSelectedTodo', todo)">{{todo.text}}</span>
          <button v-on:click="this.$emit('removeTodo', todo)">X</button>
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
