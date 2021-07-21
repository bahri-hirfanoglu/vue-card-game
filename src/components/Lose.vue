<template>
  <div class="main">
     <h1> LOSE </h1>
     <div class="image">
     <img src="../assets/lose.png">
     </div>
     <button class="restart" @click="restartGame">Restart</button>
   </div>
</template>

<script>
export default {
    methods:{
        restartGame: function(){
            this.$emit("gameOver", "app-game");
        }
    }
}
</script>

<style scoped>
.main{
    width: 800px;
    height: 500px;
    margin: auto;
    position: relative;
    flex-direction: column;
    text-align: center;
}
.image{
    padding: 20px;
}
.main img{
    width:100px;
    height: 100px;
}

</style>