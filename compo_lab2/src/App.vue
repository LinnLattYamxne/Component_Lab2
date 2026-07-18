<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <!-- <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header> -->
<!-- 
  <RouterView /> -->
  <div id="layout">
    <header>
      <div class="wrapper">
        <nav>
          <RouterLink to="/">Event</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </nav>
      </div>
    </header>

    <RouterView />
  </div>
</template>


<style>
#layout {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: graysacle;
  text-align: center;
  /* margin-top: 2rem; */
  color: #2c3e50;
}
/* nav a.router-link-exact-active {
  color: var(--color-text);
} */

/* nav a.router-link-exact-active:hover {
  background-color: transparent;
} */

nav {
  padding: 30px;
}

nav a {
  /* display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border); */
  font-weight: bold;
  color: #2c3e50;
}

/* nav a:first-of-type {
  border: 0;
} */

/* @media (min-width: 1024px) {

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
} */

 nav a.router-link-exact-active {
  color: #42b983;
 }

 h2 {
  font-size: 20px
 }
</style>
