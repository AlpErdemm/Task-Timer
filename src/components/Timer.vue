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
    <v-card elevation="16" class="ml-16 mt-6 w-75">
        <v-toolbar color="purple" class="text-center" flat dense>
            <v-toolbar-title>
                {{selectedTodo?.text}}
            </v-toolbar-title>
        </v-toolbar>
        <v-card-text>
            <h1 class="text-center" v-if="this.duration === 0">Finished!</h1>
            <div v-else class="text-center">
                <h1>{{`${Math.floor(duration / 60)} : ${(duration % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })}`}}</h1>
                <v-btn variant="contained-flat" class="mt-5 text-primary" v-on:click="this.$emit('toggleInterval')">
                    {{ this.continue ? 'Stop Timer' : 'Start Timer' }}
                </v-btn>
            </div>
        </v-card-text>
    </v-card>
</div>
</template>
