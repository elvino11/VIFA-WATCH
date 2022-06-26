<script setup>
import { RouterLink, RouterView } from "vue-router";
import HelloWorld from "@/components/HelloWorld.vue";

import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap/dist/js/bootstrap'

</script>

<template>

<!--  <header>
    <RouterLink to="/home">
      <img
        alt="Vue logo"
        class="logo"
        src="@/assets/logo.png"
        width="200"
        height="200"
      />
    </RouterLink>


    <div class="wrapper">
      <nav>
        <RouterLink to="/">Login</RouterLink>
        <RouterLink to="/register">Register</RouterLink>
        <RouterLink to="/home">Home</RouterLink>
        <RouterLink to="/product">Product</RouterLink>
        <RouterLink to="/brand">Brand</RouterLink>
        <RouterLink to="/testing">Adding</RouterLink>
        <RouterLink to="/cart">Transaction</RouterLink>
        <RouterLink to="/transaction">History Transaction</RouterLink>
        <RouterLink to="/about">About</RouterLink>


      </nav>

    </div>
  </header>-->
  <RouterView />
</template>

<style>
@import "@/assets/base.css";

#app {
  max-width: 1280px;
  margin: 0 auto;
  /*padding: 2rem;*/
  font-weight: normal;
}

header {
  /*line-height: 1.5;
  max-height: 100vh;*/
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  /*color: hsla(160, 100%, 37%, 1);*/
  color: #e54499;
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav {
  width: 100%;
  font-size: 16px;
  text-align: center;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  body {
    /*display: flex;*/
    /*margin: 0 auto;
    padding: 2rem;
    place-items: center;*/
  }

  #app {
    /*display: grid;*/
   /* grid-template-columns: 1fr 1fr;
    padding: 0 2rem;*/
  }

  /*header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }*/

  nav {
    /*text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;*/
  }
}
</style>
