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
                duration: 5,
                done: false,
            },
            tab: null,
            text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
        }
    },
      methods : {
          resetForm(){
              this.newTodo.text=''
              this.newTodo.duration=5
          }
      }
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
                    <v-text-field maxlength="30" counter="30" v-model="newTodo.text" label="Task name" variant="underlined"></v-text-field>
                </v-col>
            </v-row>

            <v-slider class="my-n6" min="5" max="60" v-model="newTodo.duration" step="5" thumb-label="always" show-ticks="always">
                <v-slider-tumb-label>
                    Ha!
                </v-slider-tumb-label>
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
            <v-row class="mt-n6" justify="end">
                <v-btn variant="contained-flat" :class="newTodo.text ? 'text-primary' : 'text-disabled' " v-on:click="this.$emit('addTodo', newTodo);resetForm();" :disabled="!newTodo.text">
                    ADD
                </v-btn>
            </v-row>
        </v-card-text>
    </v-card>
    <v-tabs v-model="tab" centered  background-color="purple" class="ml-16 mt-4 w-75">
        <v-tab value="tab-1">
            <v-icon>mdi-phone</v-icon>
            All
        </v-tab>

        <v-tab value="tab-2">
            <v-icon>mdi-heart</v-icon>
            Still going
        </v-tab>

        <v-tab value="tab-3">
            <v-icon>mdi-account-box</v-icon>
            Done
        </v-tab>
    </v-tabs>
    <v-window v-model="tab">
        <v-window-item v-for="i in 3" :key="i" :value="'tab-' + i">
            <v-card height="350" color="white" class="overflow-auto ml-16 w-75">
                <v-card v-for="todo in todos" :key="todo.id" class="my-4 w-100">
                    <div v-if="this.tab === 'tab-1' || this.tab === 'tab-2' && !todo.done || this.tab === 'tab-3' && todo.done" >
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
</div>
</template>
