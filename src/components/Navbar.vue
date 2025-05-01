<template>
  <nav class="navbar">
    <div class="navbar-container">
      <router-link to="/" class="logo">
        <svg class="aestina-logo" viewBox="0 0 300 80">
          <path d="M20,60 L40,20 L60,60 M30,45 L50,45"
                stroke="#42b983"
                stroke-width="4"
                fill="none" />
          <text x="80" y="55" font-size="42" fill="white">estina</text>
        </svg>
      </router-link>

      <div class="nav-links">
        <router-link
            v-for="link in links"
            :key="link.path"
            :to="link.path"
            class="nav-link"
        >
          {{ link.name }}
          <span class="link-underline"></span>
        </router-link>
      </div>
    </div>
  </nav>
</template>

<script setup>
const links = [
  { name: 'Home', path: '/' },
  { name: 'Projects', path: '/projects' },
  { name: 'About', path: '/about' },
  { name: 'Contact', path: '/contact' }
]
</script>

<style scoped lang="scss">
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  padding: 1rem 0;
  background: rgba(15, 32, 39, 0.8); // Dark blue glass
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(66, 185, 131, 0.3); // Accent color border

  &-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
}

.aestina-logo {
  height: 40px; /* Adjust based on your navbar */
  margin-right: 10px;
  transition: all 0.3s ease;
}

.logo:hover .aestina-logo {
  transform: scale(1.05);
  opacity: 0.9;
}

.logo {
  font-size: 1.8rem;
  font-weight: 700;
  text-decoration: none;
  display: flex;
  align-items: center;

  &-text {
    color: white;
    transition: all 0.3s ease;
  }

  &-dot {
    color: #42b983;
    transition: all 0.3s ease;
  }

  &:hover {
    .logo-text {
      color: #42b983;
    }
    .logo-dot {
      transform: scale(1.5);
    }
  }
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-link {
  color: rgba(255, 255, 255, 0.8);
  text-decoration: none;
  font-weight: 500;
  position: relative;
  padding: 0.5rem 0;
  transition: all 0.3s ease;

  .link-underline {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 0;
    height: 2px;
    background: linear-gradient(90deg, #42b983, #2c5364);
    transition: width 0.3s ease;
  }

  &:hover {
    color: white;

    .link-underline {
      width: 100%;
    }
  }

  &.router-link-exact-active {
    color: #42b983;
    font-weight: 600;

    .link-underline {
      width: 100%;
      background: #42b983;
    }
  }
}

@media (max-width: 768px) {
  .nav-links {
    gap: 1rem;
  }

  .logo {
    font-size: 1.5rem;
  }
}
</style>