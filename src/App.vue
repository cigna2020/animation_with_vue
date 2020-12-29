<template>
  <router-view v-slot="slotProps">
    <transition name="route" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
</template>

<script>
export default {
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      visibleText: false,
      usersAreVisible: false,
      enterInterval: null,
      leaveInterval: null
    };
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  transition: 0.5s all;
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.active {
  /* transform: translateX(-150px); */
  background-color: #e76f0e;
  /* border-radius: 100px; */
  animation: slide-fade 0.3s ease-out forwards;
}
/* name of animation is up to you */
@keyframes slide-fade {
  0% {
    transform: translateX(0) scale(1);
  }
  70% {
    transform: translateX(-120px) scale(1.3);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}

.button-enter-from,
.button-leave-to {
  opacity: 0;
}

.button-enter-active {
  transition: opacity 0.3s ease-out;
}

.button-leave-active {
  transition: opacity 0.3s ease-in;
}

.button-enter-to,
.button-leave-from {
  opacity: 1;
}

.route-enter-active {
  animation: slide-fade 0.4s ease-out;
}
.route-leave-active {
  animation: slide-fade 0.4s ease-in;
}
</style>
