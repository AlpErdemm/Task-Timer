<script>
export default {
    props: {
        duration: Number,
        continue: Boolean,
        selectedTodo: Object
    },
}
</script>

<template>
<div>
    <v-card class="ml-16 w-75">
        <v-toolbar color="purple" class="text-center" flat dense>
            <v-toolbar-title>
                {{selectedTodo?.text}}
            </v-toolbar-title>
        </v-toolbar>
        <v-card-text>
            <h1 v-if="this.duration === 0">Finished!</h1>
            <div v-else class="text-center">
                <h1>{{`${Math.floor(duration / 60)} : ${(duration % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })}`}}</h1>
                <v-btn class="mt-5" fab rounded color="primary" v-on:click="this.$emit('toggleInterval')">
                    {{ this.continue ? 'Stop' : 'Start' }}
                </v-btn>
            </div>
        </v-card-text>
    </v-card>
</div>
</template>
