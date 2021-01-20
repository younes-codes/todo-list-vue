<template>
  <div id="app">
    <div id="nav"></div>
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
  align-items: center;
  height: 60px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
  font-size: 1.4rem;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
