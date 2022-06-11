<script>
export default {
    props: {
        todos: Array,
        items: Array,
        selectedTodo: Object
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
<div>
    <v-card class="ml-16 w-75">
        <v-toolbar color="purple" class="text-center" flat dense>
            <v-toolbar-title>
                What would you like to do?
            </v-toolbar-title>
        </v-toolbar>

        <v-card-text>
            <v-row class="mb-4" justify="space-between">
                <v-col class="text-center">
                    <v-text-field v-model="newTodo.text" label="Task name" variant="underlined"></v-text-field>
                </v-col>
            </v-row>

            <v-slider class="my-n6" min="10" max="60" v-model="newTodo.duration" step="10" thumb-label="always">
                <template v-slot:thumb-label="{ modelValue}">
                    {{ modelValue }} Mins
                </template>
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
            <v-row class="mt-n6" justify="center">
                <v-btn class="mx-2" fab rounded color="primary" v-on:click="this.$emit('addTodo', newTodo)" :disabled="!newTodo.text">
                    <v-icon dark>
                        mdi-plus
                    </v-icon>
                </v-btn>
            </v-row>
        </v-card-text>
    </v-card>
    <v-sheet height="400" plain color="rgb(255, 0, 0, 0)" class="overflow-auto mt-3">
        <div v-for="todo in todos" :key="todo.id" class="ml-16 my-4 w-75">
            <v-progress-linear height="10" color="purple" :model-value="100 - ((todo.duration / todo.totalDuration)*100)"></v-progress-linear>
            <v-banner lines="one" color="deep-purple-accent-4" :icon="todo.id === selectedTodo?.id ? 'mdi-face':''">

                <v-banner-text>
                    {{todo.text}}
                </v-banner-text>

                <template v-slot:actions>
                    <v-btn v-on:click="this.$emit('setSelectedTodo', todo)">Select</v-btn>
                    <v-btn v-on:click="this.$emit('removeTodo', todo)">Delete</v-btn>
                </template>
            </v-banner>
        </div>
    </v-sheet>
</div>
</template>
