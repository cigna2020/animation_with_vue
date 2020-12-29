<template>
  <transition-group tag="ul" name="user-list">
    <li v-for="user in users" :key="user" @click="removeUser(user)">
      {{ user }}
    </li>
  </transition-group>
  <input type="tex" ref="inputUserName" />
  <button @click="addUser">Add User</button>
</template>

<script>
export default {
  data() {
    return {
      users: ['Max', 'Sem', 'Alex', 'Julie', 'Mane']
    };
  },
  methods: {
    addUser() {
      this.users.unshift(this.$refs.inputUserName.value);
      this.$refs.inputUserName.value = '';
    },
    removeUser(user) {
      this.users = this.users.filter(usr => usr != user);
    }
  }
};
</script>

<style scoped>
ul {
  margin: 0;
  padding: 0;
}

li {
  list-style: none;
  padding: 1rem;
  border: 1px solid #ccc;
  font-size: 18px;
}

.user-list-enter-from {
  opacity: 0;
  transform: translateX(-50px);
  background-color: yellow;
}
.user-list-enter-active {
  transition: all 1s ease-in;
  /* position: absolute; */
}
.user-list-enter-to,
.user-list-leave-from {
  opacity: 1;
  transform: translateX(0);
  background-color: none;
}
.user-list-move {
  transition: all 0.8s ease;
}

.user-list-leave-to {
  opacity: 0;
  transform: translateX(50px);
  background-color: yellow;
}
.user-list-leave-active {
  transition: all 1s ease-out;
  position: absolute;
}
</style>
