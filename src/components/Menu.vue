<template>
  <div class="menu">
      <button class="start" @click="startGame">START</button>
  </div>
</template>

<script>
export default {
    methods:{
        startGame: function(){
            this.$emit("startGame",true)
        }
    }
}
</script>

<style>
.menu{
    text-align: center;
}
.start{
    width: 150px;
    height: 50px;
    font-family: 'Trebuchet MS', 'Lucida Sans Unicode', 'Lucida Grande', 'Lucida Sans', Arial, sans-serif;
    color: #fff;
    border-style: none;
    font-size: 20px;
    font-weight: 600;
    background: crimson;
}
.start:hover{
    background: darkred;
}
</style>