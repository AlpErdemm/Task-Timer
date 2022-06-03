<script>
export default {
    props: {
        todos: Array,
    },

    data() {
        return {
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
                <span class="subheading">METRONOME</span>
            </v-toolbar-title>
            <v-spacer></v-spacer>
            <v-btn icon>
                <v-icon>mdi-share-variant</v-icon>
            </v-btn>
        </v-toolbar>

        <v-card-text>
            <v-row class="mb-4" justify="space-between">
                <v-col class="text-left">
                    <span class="text-h2 font-weight-light" v-text="bpm"></span>
                    <span class="subheading font-weight-light mr-1">BPM</span>
                    <v-fade-transition>
                        <v-avatar v-if="isPlaying" :color="color" :style="{
                animationDuration: animationDuration
              }" class="mb-1 v-avatar--metronome" size="12"></v-avatar>
                    </v-fade-transition>
                </v-col>
                <v-col class="text-right">
                    <v-btn :color="color" dark depressed fab @click="toggle">
                        <v-icon large>
                            {{ isPlaying ? 'mdi-pause' : 'mdi-play' }}
                        </v-icon>
                    </v-btn>
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
                        mdi-pluss
                    </v-icon>
                </template>
            </v-slider>
        </v-card-text>
    </v-card>
    <div class="d-flex flex-column mb-6">
        <v-card class="d-flex justify-center mb-6 align-center" height=100 color="rgba(255, 0, 0, 0.1)">
            <form @submit.prevent="this.$emit('addTodo', newTodo)">

                <input v-model="newTodo.text">

                <input type="number" v-model="newTodo.duration">

                <button>Add Task</button>

            </form>
        </v-card>
        <v-card class="d-flex justify-center mb-6 align-center" height=100 color="rgba(255, 0, 0, 0.1)">
            <ul>
                <li class="listElem" v-for="todo in todos" :key="todo.id">

                    <span @click="this.$emit('setSelectedTodo', todo)">{{todo.text}}</span>

                    <button v-on:click="this.$emit('removeTodo', todo)">X</button>

                </li>
            </ul>
        </v-card>
    </div>

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
