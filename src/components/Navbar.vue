
<script setup>
</script>

<template>
  <nav class="navbar">
    <div class="container">
      <router-link to="/" class="logo">Aestina</router-link>
      <div class="nav-links">
        <router-link to="/">Home</router-link>
        <router-link to="/about">About</router-link>
        <router-link to="/projects">Projects</router-link>
        <router-link to="/contact">Contact</router-link>
      </div>
    </div>
  </nav>
</template>


<style scoped lang="scss">
.navbar {
  background: #2c3e50;
  padding: 1rem 0;

  .container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .logo {
    color: white;
    font-weight: bold;
    font-size: 1.5rem;
    text-decoration: none;
  }

  .nav-links {
    a {
      color: white;
      margin-left: 20px;
      text-decoration: none;

      &:hover {
        color: #42b983;
      }

      &.router-link-exact-active {
        color: #42b983;
        font-weight: bold;
      }
    }
  }
}
</style>