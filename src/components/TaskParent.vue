<script>
import TaskManager from './TaskManager.vue';
import Timer from './Timer.vue';
import TaskAdder from './TaskAdder.vue';

let id = 1;

export default {
    name: 'TaskParent',

    components: {
        TaskManager,
        Timer,
        TaskAdder
    },

    data() {
        return {
            todos: [{
                id: 0,
                done:false,
                text:"This is an example task!",
                duration: 10,
                totalDuration: 10
            }],
            selectedTodo: null,
            isContinue: false,
            interval: null,
        }
    },

    methods: {
        addTodo(newTodo) {
            const {
                text,
                duration,
                done
            } = newTodo;
            this.todos.push({
                id: id++,
                done,
                text,
                duration: duration * 60,
                totalDuration: duration * 60
            });

            if (this.todos.length === 1) {
                this.setSelectedTodo(this.todos[0]);
            }
        },

        removeTodo(todo) {
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
            this.isContinue = false;
            clearInterval(this.interval);
        },

        toggleInterval() {
            this.isContinue = !this.isContinue;

            if (this.isContinue) {
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
                    oldSelectedTodo.done = true
                    clearInterval(this.interval);
                    this.isContinue = false;
                }
            },
            deep: true
        },
        todos: {
            handler(newTodos, oldTodos) {
                localStorage.setItem("todos", JSON.stringify(newTodos));
            },
            deep: true
        },
    },

    mounted() {
        if (localStorage.todos) {
            this.todos = JSON.parse(localStorage.getItem("todos"))
        }
        this.selectedTodo = this.todos[0];
    }
}
</script>

<template>
<v-sheet elevation="16" color="purple" class=" d-flex align-center" height="50">
    <p class="text-h5 pl-5">Task Timer</p>
</v-sheet>
  <v-container>
      <v-row>
          <v-col>
              <TaskManager :todos='todos' :selectedTodo='selectedTodo' @removeTodo="removeTodo" @setSelectedTodo="setSelectedTodo" />
          </v-col>
          <v-col>
              <TaskAdder @addTodo="addTodo" />
              <p v-if="!this.todos.length" class="text-center text-h5 mt-5">Add a new task to start the timer.</p>
              <Timer v-else :selectedTodo="selectedTodo" :duration="this.selectedTodo?.duration ?? 300" :isContinue="isContinue" @toggleInterval="toggleInterval" />
          </v-col>
      </v-row>
  </v-container>
</template>
