<script>
export default {
    data() {
        return {
            newTodo: {
                text: '',
                duration: 5,
                done: false,
            },
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
<div>
    <v-card elevation="16" class="ml-16 mt-4 w-75">
        <v-toolbar color="purple" class="text-center" flat dense>
            <v-toolbar-title>
                Add a new task
            </v-toolbar-title>
        </v-toolbar>

        <v-card-text>
            <v-row class="mb-4" justify="space-between">
                <v-col class="text-center">
                    <v-text-field maxlength="30" counter="30" v-model="newTodo.text" label="Task name" variant="underlined"></v-text-field>
                </v-col>
            </v-row>

            <v-slider class="my-n6" min="5" max="60" v-model="newTodo.duration" step="5" thumb-label="always" show-ticks="always">
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
</div>
</template>
