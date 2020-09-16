<template>
  <div id="app">
    <div id="nav">
      <b-container>
        <router-link to="/">Test</router-link> |
        <router-link to="/about">Stats</router-link>
      </b-container>
    </div>
    <router-view/>
    <footer>
      <b-container>
        <h5>Powered by <a href="https://alexpedrasa10.github.io/#/" style="color:#F1F1F1">Alex Pedrasa</a></h5>
      </b-container>
    </footer>
  </div>
</template>

<style>
#app {
  font-family: "Raleway";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

#nav {
  padding: 1rem;
  background: #1B618C;
  text-align: center;
}

#nav a {
  font-weight: bold;
  color: #F1F1F1;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

footer{
  padding: 1rem;
  background: #1B618C;
  color: #F1F1F1;
}

footer h5{
  text-align: center;
  text-transform: uppercase;
  font-size: 1rem;
}
</style>
