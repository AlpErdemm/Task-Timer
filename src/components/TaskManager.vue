<script>
export default {
    props: {
        todos: Array,
        selectedTodo: Object
    },

    data() {
        return {
            newTodo: {
                text: '',
                duration: 5,
                done: false,
            },
            tab: null,
        }
    },
    methods: {
        resetForm() {
            this.newTodo.text = ''
            this.newTodo.duration = 5
        }
    }
}
</script>

<template>
<v-tabs centered v-model="tab" background-color="purple" class="mt-4">
    <v-tab min-width="50" value="tab-1">
        <v-icon>mdi-clipboard-outline</v-icon>
        All
    </v-tab>

    <v-tab min-width="50" value="tab-2">
        <v-icon>mdi-clipboard-clock-outline</v-icon>
        Still going
    </v-tab>

    <v-tab min-width="50" value="tab-3">
        <v-icon>mdi-clipboard-check-outline</v-icon>
        Done
    </v-tab>
</v-tabs>
<v-window v-model="tab">
    <v-window-item v-for="i in 3" :key="i" :value="'tab-' + i">
        <v-card elevation="16" height="550" color="white" class="overflow-auto mb-6">
            <v-card v-for="todo in todos" :key="todo.id" class="my-4">
                <div v-if="this.tab === 'tab-1' || this.tab === 'tab-2' && !todo.done || this.tab === 'tab-3' && todo.done">
                    <v-progress-linear height="10" color="purple" :model-value="100 - ((todo.duration / todo.totalDuration)*100)"></v-progress-linear>
                    <v-banner lines="one" color="deep-purple-accent-4">
                        <v-banner-icon v-if="selectedTodo?.id === todo.id" icon="" size="10" class="mr-1 mt-3"></v-banner-icon>
                        <v-banner-text :class="todo.done ? 'pa-0 text-decoration-line-through' : 'pa-0'">
                            {{todo.text}}
                        </v-banner-text>

                        <template v-slot:actions>
                            <v-btn v-on:click="this.$emit('setSelectedTodo', todo)">Select</v-btn>
                            <v-btn v-on:click="this.$emit('removeTodo', todo)">Delete</v-btn>
                        </template>
                    </v-banner>
                </div>
            </v-card>
        </v-card>
    </v-window-item>
</v-window>
</template>
