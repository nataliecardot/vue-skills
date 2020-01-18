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
export default {
  name: "app"
};
</script>

<style>
@import url("https://fonts.googleapis.com/css?family=Montserrat:400,700");

* {
  box-sizing: border-box;
}

body {
  background-color: #eee;
  font-family: "Montserrat", sans-serif;
  /* display: grid (or flex) along with setting auto margin for flex item causes it to be centered */
  display: grid;
  justify-items: center;
  margin: 0;
  padding-top: 3.5rem;
}

body,
html {
  height: 100%;
}

#app {
  width: 50%;
  /* margin: auto; */
}

nav {
  padding: 20px 20px 20px 0;
}

nav a {
  padding: 0.8rem;
  text-decoration: none;
  background: #fff;
  border-radius: 3px;
  color: rgb(0, 110, 255);
  font-weight: bolder;
  margin-right: 15px;
}

@media screen and (max-width: 767px) {
  body {
    padding-top: 1rem;
  }

  #app {
    width: 90%;
  }
}
</style>
