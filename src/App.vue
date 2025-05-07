
<script setup>
import Navbar from './components/Navbar.vue'

</script>

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


<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  padding: 0;
  margin: 0;
}

.footer {
  margin-top: auto;
  background: rgba(15, 32, 39, 0.8); // Dark blue glass
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
      -webkit-tap-highlight-color: transparent;
      color: white;
      margin-left: 15px;
      text-decoration: none;

      &:hover {
        color: #42b983;
      }
    }
  }
}
@media (max-width: 768px) {
  .footer {
    padding: 0.5rem 0.5rem;
    flex-direction: column;
    align-items: center;
    font-size: small;
  }
}
</style>