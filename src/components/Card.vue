<template>
  <div class="card">
      <transition name="click" mode="out-in" appear>
      <img :src="cardimage" :key="cardimage">
      </transition>
  </div>
</template>

<script>
export default {
    props: ["cardimage"]
}
</script>

<style>
.card{
    width: 91px;
    height: 95px;
    float: left;
    padding: 5px;
    margin:7px;
}
.card img {
    width: 100%;
    height: 100%;
}

.click-enter{
    opacity: 0;
}
.click-enter-active{
    transition: opacity 0.8s;
    transition: 1;
    animation: click-enter 0.3s ease-in forwards;
}
.click-leave-active{
     transition: opacity 0.3s;
     opacity: 0;
    animation: click-leave 0.3s ease-out forwards;
}
@keyframes click-enter {
    from{
        transform: scaleY(0);
    }
    to{
        transform: scaleY(1080deg);
    }
}

@keyframes click-leave {
    from{
        transform: scaleY(1080deg);
    }
    to{
        transform: scaleY(0);
    }
}
</style>