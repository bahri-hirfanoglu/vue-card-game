<template>
  <div id="app">
    <transition name="slide-comp" mode="out-in">
    <component :is="maincomp" @gameOver="maincomp = $event"></component>
    </transition>
  </div>
</template>

<script>
import Game from "./components/Game.vue";
import Win from "./components/Win.vue"
import Lose from "./components/Lose.vue"

export default {
  name: "app",
  data() {
    return {
      maincomp: "app-game"
    };
  },
  components: {
    appGame: Game,
    appWin: Win,
    appLose: Lose
  },
};
</script>

<style>
body{
  font-family: Poppins;
  background: hsl(240deg 8% 93%);
  color: #47525d;
}
.slide-comp-enter-active{
  animation: slide-in .3s ease-out forwards;
}
.slide-comp-leave-active{
    animation: slide-out .3s ease-in forwards;
}

@keyframes slide-in {
  from{
    transform: translateX(-1000px);
    opacity: 0;
  }
  to{
    transform: translateX(0px);
    opacity: 1;
  }
}
@keyframes slide-out {
  from{
    transform: translateX(0px);
    opacity: 1;
  }
  to{
    transform: translateX(1000px);
    opacity: 0;
  }
}
.restart{
  width:200px;
  height: 50px;
  font-family: Poppins;
  border-style: none;
  font-size: 19px;
  font-weight: 500;
  background: hsl(242deg 88% 66%);
  color:#fff;
}
</style>
