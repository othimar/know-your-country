<script>
export default{
    data(){
        return{
            playerName:""
        }
    },  
    methods:{
        startGame(){
            this.$emit('onStartGame', this.playerName)
        }
    }
}
</script>

<template>
     <div class="container">
        <h1>Know your country</h1>
        <input type="text" v-model="this.playerName" placeholder="Quel est votre nom?"/>
        <button class="btn-start" @click="startGame">Commencer</button>
    </div>
</template>