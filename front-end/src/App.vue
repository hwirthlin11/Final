<template>
<div id="app">
  <div class="header">
    <div class="brand">
      <h1>Bloomin' Acres Flower Farm</h1>
    </div>
  </div>
  <div class="content">
    <router-view />
  </div>
</div>
</template>

<style>
body {
  margin: 0px;
  background: #ebfcfb;
}

#app {
  font-family: monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}


.brand {
  display: flex;
  background: #023047;
  padding: 10px 100px;
}

.brand h1 {
  display: inline-block;
  background: #023047;
  padding: 10px;
  font-size: 30px;
  color:white;
}

.main {
  padding: 20px 100px;
}

.pure-button {
  font-size: 10px;
}

h1 {
  font-size: 16px;
}

h2 {
  font-size: 12px;
}

.space-right {
  margin-right: 10px;
}

a {
  color: #023047;
}

.pure-button-primary {
  background-color: #black;
  color: #333;
  font-size: 20px;
}
</style>
