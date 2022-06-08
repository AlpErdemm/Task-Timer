<script>
export default {
    props: {
        duration: Number,
        continue: Boolean,
    },
}
</script>

<template>
<div>
<v-card class="ml-16 w-75" >
    <v-toolbar color="purple" class="text-center" flat dense> </v-toolbar>
    <v-card-text >
            <h1 v-if="this.duration === 0">Finished!</h1>
            <div v-else class="text-center">
                <h1>{{`${Math.floor(duration / 60)} : ${(duration % 60).toLocaleString(undefined, { minimumIntegerDigits: 2 })}`}}</h1>
                <button @click="this.$emit('toggleInterval')">
                    {{ this.continue ? 'Stop' : 'Start' }}
                </button>
            </div>
    </v-card-text>
</v-card>
</div>
</template>
