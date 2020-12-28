<template>
  <ul>
    <li v-for="user in users" :key="user" @click="removeUser(user)">
      {{ user }}
    </li>
  </ul>
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
</style>
