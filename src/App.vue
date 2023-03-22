
<template>
  <div>
    <router-link to="/">Home</router-link> |
    <router-link to="/about">Inventory</router-link>
  </div>
  <router-view/>
</template>

<script>
import HomeView from './views/HomeView.vue';
import {  RouterView } from 'vue-router'

export default{
components:{
  HomeView
}
}



</script>

<style scoped>



header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
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

</style>
