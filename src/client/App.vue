<template>
  <div id="app">
    <router-link to="/survey/admin">Create Survey</router-link> |
    <router-link to="/survey">Survey</router-link> |
    <router-link to="/survey/results/:id">Survey Results</router-link>
    <router-view />
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  h2,
  h3 {
    font-weight: normal;
  }
  button,
  a,
  li,
  input {
    cursor: pointer;
  }

  a {
    text-decoration: none;
    color: black;
  }
  ul {
    padding: 0;
  }
}
</style>
