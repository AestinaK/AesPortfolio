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

        <button class="mobile-menu-btn" @click="toggleMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
    </div>
    <div class="mobile-menu" :class="{ active: isMenuOpen }">
      <router-link to="/" @click="isMenuOpen = false">Home</router-link>
      <router-link to="/projects" @click="isMenuOpen = false">Projects</router-link>
      <router-link to="/about" @click="isMenuOpen = false">About</router-link>
      <router-link to="/contact" @click="isMenuOpen = false">Contact</router-link>
    </div>
  </nav>
</template>

<script setup>

import {ref} from "vue";

const isMenuOpen=ref(false);
const links = [
  { name: 'Home', path: '/' },
  { name: 'Projects', path: '/projects' },
  { name: 'About', path: '/about' },
  { name: 'Contact', path: '/contact' }
]
const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
}
</script>

<style scoped lang="scss">
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  padding: 1rem 0;
  background: rgba(15, 32, 39, 0.8);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(66, 185, 131, 0.3);

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
  height: 40px;
  margin-right: 10px;
  transition: all 0.3s ease;
}

.logo:hover .aestina-logo {
  transform: scale(1.05);
  opacity: 0.9;
}

.logo {
  -webkit-tap-highlight-color: transparent;
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
  gap: 1rem;
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

.mobile-menu-btn {
  display: none;
  background: none;
  border: none;
  color: white;
  font-size: 1.5rem;
  cursor: pointer;
  -webkit-tap-highlight-color: transparent;
  &:active, &:focus {
    outline: none !important;
  }
}

.mobile-menu {
  display: none;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  background: linear-gradient(135deg, #68c39a, #2c5364);
  color: white;
  padding: 1rem;
  flex-direction: column;
  gap: 1rem;
  z-index: 1000;
  box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
  border-radius: 0 0 8px 8px;
}
.mobile-menu a{
  color: white;
  text-decoration: none;
  transition: color 0.3s ease;
  display: block;
  padding: 5px 10px;
  border: none;
  -webkit-tap-highlight-color: transparent;
}

.mobile-menu a.router-link-exact-active {
  color: #42b983;
  font-weight: bold;
}
.mobile-menu.active {
  display: flex;
  color: rgba(255, 255, 255, 0.8);
}

.mobile-menu a:active {
  background-color: transparent !important;
}

.mobile-menu a:active,
.mobile-menu a:focus {
  background: transparent !important;
}

@media (max-width: 768px) {

  .nav-links {
    display: none;
  }

  .mobile-menu-btn {
    display: block;
  }

  .mobile-menu-btn span {
    display: block;
    width: 25px;
    height: 3px;
    background: white;
    margin: 5px 0;
    transition: all 0.3s ease;
    -webkit-tap-highlight-color: transparent;
  }



}
</style>