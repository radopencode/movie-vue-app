<template>
  <nav>
    <router-link to="/">Home</router-link>
    |
    <router-link to="/about">About</router-link>
    |
    <router-link to="/movies">All movies</router-link>
    |
    <router-link to="/movies/new">New movie</router-link>
    |
    <router-link to="/signup">Signup</router-link>
    |
    <router-link>to="/login">Login</router-link>
    |
    <router-link>to="/logout>Logout</router-link>
    <span v-if="isLoggedIn()">
      <router-link to="/logout">Logout</router-link>
    </span>
    <span v-else>
      <router-link to="/signup">Signup</router-link>
      <router-link to="/login">Login</router-link>
    </span>
  </nav>
  <router-view />
</template>

<script>
methods: {
  isLoggedIn: function() {
    return localStorage.getItem('jwt');
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
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
