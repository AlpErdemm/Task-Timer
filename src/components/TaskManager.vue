<script>
export default {
    props: {
        todos: Array,
        items: Array
    },

    data() {
        return {
            newTodo: {
                text: 'New Todo',
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
        <v-toolbar flat dense>
            <v-toolbar-title>
                <input v-model="newTodo.text" placeholder="Task name?" maxlength="20" style="width: 1000px">
            </v-toolbar-title>
        </v-toolbar>

        <v-card-text>
            <v-row class="mb-4" justify="space-between">
                <v-col class="text-center">
                    <span class="text-h4 font-weight-light" v-text="newTodo.duration"></span>
                    <span class="subheading font-weight-light mr-1">Min of</span>
                    <span class="text-h4 font-weight-light">{{newTodo.text}}</span>
                </v-col>
            </v-row>

            <v-slider v-model="newTodo.duration" step="10" tick-size="4">
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
            <v-row class="mb-4" justify="center">
                <v-btn class="mx-2" fab rounded color="primary" v-on:click="this.$emit('addTodo', newTodo)">
                    <v-icon dark>
                        mdi-plus
                    </v-icon>
                </v-btn>

            </v-row>
        </v-card-text>
    </v-card>
    <v-banner lines="one" color="deep-purple-accent-4" class="my-4" v-for="todo in todos" :key="todo.id" :icon="todo.icon">
        <v-banner-text>
            {{todo.text}}
        </v-banner-text>

        <template v-slot:actions>
            <v-btn v-on:click="this.$emit('setSelectedTodo', todo)">Select</v-btn>
            <v-btn v-on:click="this.$emit('removeTodo', todo)">Delete</v-btn>
        </template>
    </v-banner>
</div>
</template>
