<script>
export default {
    props: {
        todos: Array,
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
    <v-card class="mx-auto" max-width="600">
        <v-list shaped>
                <template v-for="todo in todos" :key="todo.id">
                    <v-list-item three-line>
                            <v-chip color="primary">{{`${Math.floor(todo.duration / 60)} : ${(todo.duration % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })}`}}</v-chip>
                            <v-list-item-title class="text-h5 mb-1">
                                {{todo.text}}
                            </v-list-item-title>
                            <v-btn class="mx-2" small color="primary" rounded v-on:click="this.$emit('setSelectedTodo', todo)">
                                Select
                            </v-btn>
                    </v-list-item>

                    <v-btn class="mx-2" small color="primary" rounded v-on:click="this.$emit('removeTodo', todo)">
                        <v-icon dark>
                            mdi-minus
                        </v-icon>
                    </v-btn>
                </template>
        </v-list>
    </v-card>

</div>
</template>
