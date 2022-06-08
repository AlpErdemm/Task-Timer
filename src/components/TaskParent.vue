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
          { id: id++, done: true, text: "This is task!", duration: 10, totalDuration: 10},
          { id: id++, done: false, text: "Looks like there is more??", duration: 600, totalDuration: 600},
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
        this.todos.push({ id: id++, done, text, duration: duration * 60, totalDuration: duration * 60 });
        console.log(this.todos)

        if (this.todos.length === 1) {
          this.setSelectedTodo(this.todos[0]);
        }
      },

      removeTodo(todo){
        console.log("Remove!")
        this.todos = this.todos.filter((t) => t !== todo)

        if (todo.id === this.selectedTodo.id && this.todos.length) {
          this.setSelectedTodo(this.todos[0]);
        }
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
      },
    },

    mounted() {
      this.selectedTodo = this.todos[0];
    }
  }
</script>

<template>
  <div>
        <v-container
    >
      <v-row
        align="center"
      >
        <v-col>
    <TaskManager
      :todos='todos'
      :selectedTodo='selectedTodo'
      @addTodo="addTodo"
      @removeTodo="removeTodo"
      @setSelectedTodo="setSelectedTodo"
    />
     </v-col>
      <v-col >
    <h1 v-if="!this.todos.length">Add a new task to start the timer.</h1>
    <Timer
      v-else
      :duration="this.selectedTodo?.duration ?? 300"
      :continue="continue"
      @toggleInterval="toggleInterval"
    />
     </v-col>
      </v-row>
        </v-container>
  </div>
</template>
