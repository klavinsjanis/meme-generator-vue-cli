<template>
  <div id="app">
    <div id="title">
      <h2>MEME CREATOR</h2>
    </div>
    <router-view />
  </div>
</template>

<style>
#nav {
  padding: 30px;
  background-color: salmon;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

#title {
  text-align: center;
}
</style>
