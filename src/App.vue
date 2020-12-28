<template>
  <div class="container">
    <UsersList></UsersList>
  </div>
  <div class="container">
    <div class="block" :class="{ active: animatedBlock }"></div>
    <button @click="animateBlock">
      Animate
    </button>
  </div>
  <div class="container">
    <!-- :css="false" doesn't require but it says Vue even doesn't try to find css -->
    <transition
      :css="false"
      @before-enter="beforeEnter"
      @enter="enter"
      @after-enter="afterEnter"
      @before-leave="beforeLeave"
      @leave="leave"
      @after-leave="afterLeave"
      @enter-cancelled="enterCancelled"
      @leave-cancelled="leaveCancelled"
    >
      <p v-if="visibleText">
        This text shoud move, more text, more...
      </p>
    </transition>
    <button @click="toggleText">Move text!</button>
  </div>
  <div class="container">
    <transition name="button" mode="out-in">
      <button @click="showUsers" v-if="!usersAreVisible">Show Users</button>
      <button @click="hideUsers" v-else>Hide Users</button>
    </transition>
  </div>
  <!-- <base-modal @close="hideDialog" v-if="dialogIsVisible"> -->
  <base-modal @close="hideDialog" :open="dialogIsVisible">
    <p>This is a test dialog!</p>
    <button @click="hideDialog">Close it!</button>
  </base-modal>
  <div class="container">
    <button @click="showDialog">Show Dialog</button>
  </div>
</template>

<script>
import UsersList from './components/UsersList';
export default {
  components: {
    UsersList
  },
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      visibleText: false,
      usersAreVisible: false,
      enterInterval: null,
      leaveInterval: null
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBlock() {
      this.animatedBlock = !this.animatedBlock;
    },
    toggleText() {
      this.visibleText = !this.visibleText;
    },
    showUsers() {
      this.usersAreVisible = true;
    },
    hideUsers() {
      this.usersAreVisible = false;
    },
    beforeEnter(el) {
      console.log('before enter');
      //   console.log(el);
      el.style.opacity = 0;
    },
    enter(el, done) {
      let round = 1;
      this.enterInterval = setInterval(() => {
        el.style.opacity = round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.enterInterval);
          done(); // to controle after-enter
        }
      }, 20);
    },
    beforeLeave(el) {
      el.style.opacity = 1;
    },
    leave(el, done) {
      let round = 1;
      this.leaveInterval = setInterval(() => {
        el.style.opacity = 1 - round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(this.leaveInterval);
          done(); // without 'done' after-leave starts immediately
        }
      }, 20);
    },
    afterLeave(el) {
      console.log('after Leave');
      console.log(el);
    },
    enterCancelled() {
      clearInterval(this.enterInterval);
    },
    leaveCancelled() {
      clearInterval(this.leaveInterval);
    }
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
</style>
