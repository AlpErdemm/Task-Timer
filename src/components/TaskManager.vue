<script>
export default {
    props: {
        todos: Array,
    },

    data() {
        return {
            items: [
                'Dog Photos',
                'Cat Photos',
                '',
                'Potatoes',
                'Carrots',
            ],
            model: ['Carrots'],
            newTodo: {
                text: 'New Todo',
                duration: 5,
                done: false,
            },
            bpm: 40,
            interval: null,
            isPlaying: false,
        }
    },
    computed: {
        color() {
            if (this.bpm < 100) return 'indigo'
            if (this.bpm < 125) return 'teal'
            if (this.bpm < 140) return 'green'
            if (this.bpm < 175) return 'orange'
            return 'red'
        },
        animationDuration() {
            return `${60 / this.bpm}s`
        },
    },
    methods: {
        decrement() {
            this.bpm--
        },
        increment() {
            this.bpm++
        },
        toggle() {
            this.isPlaying = !this.isPlaying
        },
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
                    <span class="text-h4 font-weight-light" v-text="bpm"></span>
                    <span class="subheading font-weight-light mr-1">Min of</span>
                    <span class="text-h4 font-weight-light">{{newTodo.text}}</span>
                </v-col>
            </v-row>

            <v-slider v-model="bpm" step="10" ticks="always" tick-size="4">
                <template v-slot:prepend>
                    <v-icon :color="color" @click="decrement">
                        mdi-minus
                    </v-icon>
                </template>

                <template v-slot:append>
                    <v-icon :color="color" @click="increment">
                        mdi-plus
                    </v-icon>
                </template>
            </v-slider>
            <v-row class="mb-4" justify="center">
                <v-btn class="mx-2" fab dark color="indigo" v-on:click="this.$emit('addTodo', newTodo)">
                    <v-icon dark>
                        mdi-plus
                    </v-icon>
                </v-btn>

            </v-row>
        </v-card-text>
    </v-card>
    <v-card class="mx-auto" max-width="600">
        <v-list shaped>
            <v-list-item-group v-model="model" multiple>
                <template v-for="todo in todos" :key="todo.id">
                    <v-list-item-content>
                        <v-row>
                            <v-list-item-title v-text="todo.text"></v-list-item-title>
                            <button v-on:click="this.$emit('removeTodo', todo)">X</button>
                        </v-row>
                        <v-card class="d-flex align-start flex-column">
                           Something! </v-card>
                    </v-list-item-content>
                </template>
            </v-list-item-group>
        </v-list>
    </v-card>

</div>
</template>

<style>
.taskManagerPlaceholder {
    color: white;
    text-align: center;
}

.listElem {
    color: white;
    text-align: center;
}

form {
    display: flex;
    justify-content: center;
}

@keyframes metronome-example {
    from {
        transform: scale(.5);
    }

    to {
        transform: scale(1);
    }
}

.v-avatar--metronome {
    animation-name: metronome-example;
    animation-iteration-count: infinite;
    animation-direction: alternate;
}
</style>
