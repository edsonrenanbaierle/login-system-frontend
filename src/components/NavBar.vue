<template>
  <nav>
    <router-link to="/home">Home</router-link> |
    <router-link to="/">Login</router-link>
  </nav>
  <router-view />
</template>

<script>
export default {
  name: "NavBar",
};
</script>
