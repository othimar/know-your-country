<script>

export default {
    props: {
        question: Object,
        questionId: Number,
        numberOfQuestions: Number
    },
    emits: ['quit', 'answer'],
    data() {
        return {
            localPropositions: [],
        }
    },

    methods: {
        onQuit() {
            this.$emit('quit')
        },
        onAnswer(id) {
            // console.log('chosen id ', id)
            // console.log('localPropositions ', this.localPropositions)
            const id_answer = this.question.propositions.findIndex((el) => this.localPropositions[id] == el)
            // console.log('answered_id ', id_answer)
            // console.log('question proposition', this.question.propositions)
            this.$emit('answer', id_answer)
        },
        updateChanges() {
            this.localPropositions = [...this.question.propositions];
            this.localPropositions = this.localPropositions.sort(() => Math.random() - 0.5);

        }
    }, watch: {
        question() { this.updateChanges() }
    },
    mounted() {
        // console.log('mounted called')
        this.updateChanges();
    },
}
</script>

<template>
    <header>
        <div>Question {{ questionId }}/{{ numberOfQuestions }}</div>
        <button class="quit" @click="onQuit()">Quitter</button>
    </header>

    <h2 class="question">{{ question.question }}</h2>

    <div class="propositions">
        <button v-for="(proposition, index) in localPropositions" class="choice" @click="onAnswer(index)">{{
                proposition
        }}</button>
    </div>
</template>