<template>
  <div id="app">
    <nav>
      <router-link to="/">Home</router-link>
      <router-link to="/about">About</router-link>
    </nav>

    <!-- Have to use this wherever you want router to display template -->
    <router-view />
  </div>
</template>

<script>
import Skills from './components/Skills.vue';

export default {
  name: 'app',
  components: {
    Skills
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');

* {
  box-sizing: border-box;
}

body {
  background-color: #eee;
  font-family: 'Montserrat', sans-serif;
  /* display; flex along with setting auto margin for flex item causes it to be centered */
  display: grid;
  justify-items: center;
  padding-top: 50px;
}

body,
html {
  height: 100%;
}

#app {
  width: 50%;
  margin: auto;
}

nav {
  padding: 20px 20px 20px 0;
}

nav a {
  padding: 10px;
  text-decoration: none;
  background: #fff;
  border-radius: 3px;
  color: rgb(0, 110, 255);
  margin-right: 15px;
}
</style>
