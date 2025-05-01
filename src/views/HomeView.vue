<template>
  <div class="home-page">
    <!-- Shared decorative elements -->
    <div class="decor-circle circle-1"></div>
    <div class="decor-circle circle-2"></div>
    <div class="decor-blob"></div>

    <div class="content-container">
      <!-- Hero section -->
      <section class="hero-section">
        <div class="hero-content">
          <h1 class="title">
            <span class="greeting">Hello World!</span>
            <Typewriter
                :texts="typewriterTexts"
                :speed="100"
            />
          </h1>

          <p class="subtitle">
            Crafting robust solutions with <span class="highlight">.NET</span> and <span class="highlight">Vue.js</span>
          </p>

          <div class="cta-buttons">
            <router-link to="/projects" class="cta-button primary">
              View My Work
            </router-link>
            <router-link to="/contact" class="cta-button secondary">
              Contact Me
            </router-link>
          </div>
        </div>

        <div class="hero-image">
          <div class="image-container">
            <img src="../assets/developer-illustration.svg" alt="Developer Illustration" />
          </div>
        </div>
      </section>

      <!-- Skills section -->
      <section class="skills-section">
        <h2 class="section-title">Technical Expertise</h2>

        <div class="skills-grid">
          <div v-for="(category, index) in skills" :key="index" class="skill-category glow-card">
            <h3>{{ category.name }}</h3>
            <ul>
              <li v-for="(skill, skillIndex) in category.items" :key="skillIndex">
                {{ skill }}
              </li>
            </ul>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Typewriter from '../components/Typewriter.vue'

const typewriterTexts = ref([
  "I'm Aestina ",
  "A .NET Developer",
  "A Problem Solver",
  "A Full-stack Engineer"
])

const skills = ref([
  {
    name: 'Backend',
    items: [
      'C# / .NET Core',
      'ASP.NET MVC/WebAPI',
      'Entity Framework',
      'SQL Server',
      'Microservices',
        'PosgreSql'
    ]
  },
  {
    name: 'Frontend',
    items: [
      'Vue.js 3',
      'TypeScript',
      'Vite',
      'Pinia',
      'Tailwind CSS',
        'Bootstrap'
    ]
  },
  {
    name: 'DevOps & Tools',
    items: [
      'RESTful API',
      'Docker',
      'Git',
      'CI/CD Pipelines',
      'Visual Studio'
    ]
  }
])
</script>

<style scoped lang="scss">
@import "../assets/styles/_shared.scss";

.home-page {
  @extend %base-page-style;

  .content-container {
    display: flex;
    flex-direction: column;
    gap: 5rem;
  }

  .hero-section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 3rem;
    align-items: center;
  }

  .hero-content {
    .title {
      font-size: 3.5rem;
      line-height: 1.2;
      margin-bottom: 1.5rem;

      .greeting {
        display: block;
        font-size: 2rem;
        color: #42b983;
        margin-bottom: 0.5rem;
      }
    }

    .subtitle {
      font-size: 1.5rem;
      color: rgba(255, 255, 255, 0.8);
      margin-bottom: 2.5rem;

      .highlight {
        color: #42b983;
        font-weight: 500;
      }
    }
  }

  .cta-buttons {
    display: flex;
    gap: 1.5rem;
    margin-top: 2rem;
    margin-left: 5rem;

    .cta-button {
      padding: 0.8rem 1.8rem;
      border-radius: 50px;
      font-weight: 500;
      text-decoration: none;
      transition: all 0.3s ease;
      display: inline-flex;
      align-items: center;
      justify-content: center;

      &.primary {
        background: linear-gradient(135deg, #42b983, #2c5364);
        color: white;

        &:hover {
          transform: translateY(-3px);
          box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
      }

      &.secondary {
        background: transparent;
        color: #42b983;
        border: 2px solid #42b983;

        &:hover {
          background: rgba(66, 185, 131, 0.1);
        }
      }
    }
  }

  .hero-image {
    margin-top: 2rem;
    .image-container {
      position: relative;
      padding-top: 100%;
      border-radius: 20px;
      overflow: hidden;
      background: rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.1);

      img {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: contain;
        padding: 1.5rem;
      }
    }
  }

  .skills-section {
    .section-title {
      text-align: center;
      font-size: 2.5rem;
      margin-bottom: 3rem;
      position: relative;
      display: inline-block;
      left: 50%;
      transform: translateX(-50%);

      &::after {
        content: '';
        position: absolute;
        bottom: -10px;
        left: 0;
        width: 100%;
        height: 3px;
        background: linear-gradient(90deg, transparent, #42b983, transparent);
      }
    }
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
  }

  .skill-category {
    background: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    border-radius: 15px;
    padding: 2rem;
    border: 1px solid rgba(255, 255, 255, 0.1);
    transition: transform 0.3s ease;

    &:hover {
      transform: translateY(-5px);
    }

    h3 {
      color: #42b983;
      font-size: 1.5rem;
      margin-bottom: 1.5rem;
      position: relative;
      padding-bottom: 0.5rem;

      &::after {
        content: '';
        position: absolute;
        bottom: 0;
        left: 0;
        width: 50px;
        height: 2px;
        background: #42b983;
      }
    }

    ul {
      list-style: none;
      padding: 0;

      li {
        padding: 0.5rem 0;
        position: relative;
        padding-left: 1.5rem;

        &::before {
          content: '▹';
          position: absolute;
          left: 0;
          color: #42b983;
        }
      }
    }
  }
}

/* Responsive adjustments */
@media (max-width: 1024px) {
  .hero-section {
    grid-template-columns: 1fr !important;
    text-align: center;
    gap: 2rem !important;
  }

  .cta-buttons {
    justify-content: center;
  }

  .hero-image {
    order: -1;
    max-width: 400px;
    margin: 0 auto;
  }
}

@media (max-width: 576px) {
  .cta-buttons {
    flex-direction: column;
  }

  .skills-grid {
    grid-template-columns: 1fr !important;
  }
}
</style>