<template>
  <div id="app">
    <router-view></router-view> <!-- This renders the matched component -->
  </div>
</template>
<script>
import axios from './plugins/axios';

export default {
  name: 'App',
  data() {
    return {
      users: []
    }
  },
  mounted() {
    this.getUsers(); // Fetch users when the component is mounted
  },
  methods: {
    async getUsers() {
      try {
        const response = await axios.get('/users'); // Adjust the endpoint if needed
        this.users = response.data;
      } catch (error) {
        console.error('Error fetching users:', error);
      }
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
