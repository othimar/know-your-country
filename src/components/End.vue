<script>

export default {
    props: {
        score: Number,
        total: Number,
        playerName: String
    },

    methods: {
        restart() {
            this.$emit('restart')
        }
    }
}
</script>

<template>
    <div class="container">
        <h1>Terminé</h1>
        <h2>Bravo {{ playerName }}!Vous avez obtenu {{ score }}/{{ total }}</h2>
        <button class="btn-start" @click="restart">Recommencer</button>
    </div>
</template>