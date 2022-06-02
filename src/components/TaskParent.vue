<script>
  import TaskManager from './TaskManager.vue';
  import Timer from './Timer.vue';

  let id = 0;

  export default {
    name: 'TaskParent',

    components: {
      TaskManager,
      Timer
    },

    data(){
      return {
        todos : [
          { id: id++, done: true, text: "This is task!", duration: 10 },
          { id: id++, done: false, text: "Looks like there is more??", duration: 600 },
        ],
        selectedTodo : null,
        continue: false,
        interval: null,
      }
    },

    methods : {
      addTodo(newTodo){
        console.log("Add!")
        const { text, duration, done } = newTodo;
        this.todos.push({ id: id++, done, text, duration: duration * 60 });
        console.log(this.todos)
      },

      removeTodo(todo){
        console.log("Remove!")
        this.todos = this.todos.filter((t) => t !== todo)
      },

      updateRemainingTime() {
        this.interval = setInterval(() => {
          this.selectedTodo.duration--;
        }, 1000);
      },

      setSelectedTodo(todo) {
        this.selectedTodo = todo;
        this.continue = false;
        clearInterval(this.interval);
      },

      toggleInterval() {
        this.continue = !this.continue;

        if (this.continue) {
          this.updateRemainingTime();
        } else {
          clearInterval(this.interval);
        }
      }
    },

    watch: {
      selectedTodo: {
        handler(newSelectedTodo, oldSelectedTodo) {
          if (oldSelectedTodo?.duration === 0) {
            clearInterval(this.interval);
            this.continue = false;
          }
        },
        deep: true
      }
    },

    mounted() {
      this.selectedTodo = this.todos[0];
    }
  }
</script>

<template>
  <div class="grid-container">
    <TaskManager
      :todos='todos'
      @addTodo="addTodo"
      @removeTodo="removeTodo"
      @setSelectedTodo="setSelectedTodo"
    />
    <Timer
      :duration="this.selectedTodo?.duration ?? 300"
      :continue="continue"
      @toggleInterval="toggleInterval"
    />
  </div>
</template>

<style>
  .grid-container {
    display: grid;
    grid-template-columns: auto auto;
    height: 800px;
    grid-gap: 10px;
    padding: 10px;
    column-gap: 50px;
    align-items: center;
  }
</style>