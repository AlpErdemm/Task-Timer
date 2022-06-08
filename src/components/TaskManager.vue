<script>
export default {
    props: {
        todos: Array,
        items: Array
    },

    data() {
        return {
            newTodo: {
                text: '',
                duration: 10,
                done: false,
            },
        }
    },
}
</script>

<template>
<div class="TaskManager">
    <v-card class="mx-auto" max-width="600">
        <v-toolbar color="purple" class="text-center" flat dense>
            <v-toolbar-title>
                What would you like to do?
            </v-toolbar-title>
        </v-toolbar>

        <v-card-text>
            <v-row class="mb-4" justify="space-between">
                <v-col class="text-center">
                    <v-text-field v-model="newTodo.text" label="Task name" variant="underlined"></v-text-field>
                    <span class="text-h4 font-weight-light" v-text="newTodo.duration"></span>
                    <span class="subheading font-weight-light mr-1">Min</span>
                </v-col>
            </v-row>

            <v-slider min="10" max="60" v-model="newTodo.duration" step="10" tick-size="4">
                <template v-slot:prepend>
                    <v-icon>
                        mdi-minus
                    </v-icon>
                </template>

                <template v-slot:append>
                    <v-icon>
                        mdi-plus
                    </v-icon>
                </template>
            </v-slider>
            <v-row v-if="newTodo.text != ''" class="mb-4" justify="center">
                <v-btn class="mx-2" fab rounded color="primary" v-on:click="this.$emit('addTodo', newTodo)">
                    <v-icon dark>
                        mdi-plus
                    </v-icon>
                </v-btn>
            </v-row>
            <v-row v-else class="mb-4" justify="center">
                <v-btn disabled class="mx-2" fab rounded color="primary" v-on:click="this.$emit('addTodo', newTodo)">
                    <v-icon dark>
                        mdi-plus
                    </v-icon>
                </v-btn>
            </v-row>
        </v-card-text>
    </v-card>

    <div v-for="todo in todos" :key="todo.id"  class="mx-auto my-4 w-75"  >
        <v-progress-linear height="10" color="purple" :model-value="100 - ((todo.duration / todo.totalDuration)*100)"></v-progress-linear>
        <v-banner lines="one" color="deep-purple-accent-4" :icon="todo.icon">

            <v-banner-text>
                {{todo.text}}
            </v-banner-text>

            <template v-slot:actions>
                <v-btn v-on:click="this.$emit('setSelectedTodo', todo)">Select</v-btn>
                <v-btn v-on:click="this.$emit('removeTodo', todo)">Delete</v-btn>
            </template>
        </v-banner>
    </div>
</div>
</template>
