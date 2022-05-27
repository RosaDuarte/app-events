<template>
  <div class="is-flex">
    <div id="one"></div>
    <div id="two"></div>
    <div id="three"></div>
    <div id="four"></div>
    <div id="five"></div>
    <div id="six"></div>
  </div>
    
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div> -->
  <!-- <router-view /> -->
  <div class="container">
    <router-view />
  </div>
</template>


<script>

export default{
  name: "App",
  }
</script>


<style>
:root{
  --gray: #e1e0de;
  --blue-light: #7fbbc5;
  --blue: #0B3B59;
  --blue-dark: #2C5973;
  --text: #518EA6;
  --highlight: #79C7D9;
  --white: #FFF8F5;
}
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body{
  width: 100%;
  min-height: 100vh;
  background-color: var(--white);
  font-family: 'Roboto', sans-serif;
}
#one{
  width: 20%;
  height: 40px;
  background-color: var(--highlight);
}
#two{
  width: 20%;
  height: 80px;
  background-color: var(--blue);
}
#three{
  width: 20%;
  height: 60px;
  background-color: var(--text);
}
#four{
  width: 20%;
  height: 40px;
  background-color: var(--blue-dark);
}
#five{
  width: 20%;
  height: 80px;
  background-color: var(--highlight);
}
#six{
  width: 20%;
  height: 60px;
  background-color: var(--blue);
}
</style>
