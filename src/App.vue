<template>
  <div class="app">
    <nav>
      <ul>
        <li>
          <router-link to="/location" class="nav-link" :class="{ active: $route.path === '/location' }">Location</router-link>
        </li>
        <li>
          <router-link to="/stopwatch" class="nav-link" :class="{ active: $route.path === '/stopwatch' }">Stopwatch</router-link>
        </li>
        <li>
          <router-link to="/weather" class="nav-link" :class="{ active: $route.path === '/weather' }">Weather</router-link>
        </li>
        <li>
          <router-link to="/tictactoe" class="nav-link" :class="{ active: $route.path === '/tictactoe' }">Tic Tac Toe</router-link>
        </li>
        <li>
          <router-link to="/photo" class="nav-link" :class="{ active: $route.path === '/photo' }">Photo</router-link>
        </li>
      </ul>
    </nav>
    <div class="content">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
}

nav {
  background-color: #f2f2f2;
  display: flex;
  justify-content: center;
  padding: 30px;
}

nav ul {
  list-style: none;
  display: flex;
  margin: auto;
  padding: auto;
}

nav ul li {
  margin-right: 10px;
}

nav ul li a {
  display: flex;
  height: 0.1px;
  background: black;
  transition: all 0.3s;
}

nav ul li a:hover {
  transform: scale(1.1);
}

.nav-list {
  list-style: none;
  justify-content: center;
}

.nav-list li {
  margin-right: 20px;
}

.nav-link {
  text-decoration: none;
  color: #1976d2;
}

.nav-link:active {
  color: black;
  transform: scale(0.9);
  transition: transform 0.2s ease;
}

.active {
  color: black;
  background-color: #2196f3;
}
</style>
