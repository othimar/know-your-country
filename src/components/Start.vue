<script>
export default {
    data() {
        return {
            playerName: "",
            playerNameisValid: true,
        };
    },
    methods: {
        nameCheck() {
            this.playerNameisValid = this.playerName != "" ? true : false;
        },
        startGame() {
            // console.log('playerName is : ', this.playerName);
            // console.log('playerNameisValid is : ', this.playerNameisValid);
            this.nameCheck()
            if (this.playerNameisValid) {
                this.$emit("onStartGame", this.playerName);
            }
        },
    },
};
</script>
 
<template>
    <div class="container">
        <h1>Know your country</h1>
        <p v-if="!playerNameisValid">veuillez entrer votre nom svp!</p>
        <input type="text" v-model="playerName" placeholder="Quel est votre nom?" @keypress.enter="startGame" />
        <button class="btn-start" @click="startGame">Commencer</button>
    </div>
</template>

<style>

</style>