<template>
  <Navbar />
  <router-view />
  <footer class="footer">
    <div class="container">
      <p>© {{ new Date().getFullYear() }} Aestina Katwal. All rights reserved.</p>
      <div class="social-links">
        <a href="https://github.com/AestinaK" target="_blank">GitHub</a>
        <a href="https://www.linkedin.com/in/aestina-katwal-040036249/" target="_blank">LinkedIn</a>
        <a href="https://twitter.com/yourusername" target="_blank">Twitter</a>
      </div>
    </div>
  </footer>
</template>

<script>
import Navbar from './components/Navbar.vue'

export default {
  name: 'App',
  components: {
    Navbar
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

.footer {
  margin-top: auto;
  background: #2c3e50;
  color: white;
  padding: 20px 0;

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .social-links {
    a {
      color: white;
      margin-left: 15px;
      text-decoration: none;

      &:hover {
        color: #42b983;
      }
    }
  }
}
</style>