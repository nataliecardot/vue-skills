<template>
  <div id="app">
    <Skills />
  </div>
</template>

<script>
import Skills from "./components/Skills.vue";

export default {
  name: "app",
  components: {
    Skills
  }
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");
body {
  background-color: #eee;
  font-family: "Montserrat", sans-serif;
  /* display; flex along with setting auto margin for flex item causes it to be centered */
  display: flex;
  margin: 0;
  padding: 2rem;
}

body,
html {
  height: 100%;
}

#app {
  width: 50%;
  margin: auto;
}

* {
  box-sizing: border-box;
}
</style>
