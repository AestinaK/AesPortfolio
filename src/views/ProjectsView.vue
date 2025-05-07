<template>
  <div class="projects-page">
    <!-- Shared decorative elements -->
    <div class="decor-circle circle-1"></div>
    <div class="decor-circle circle-2"></div>
    <div class="decor-blob"></div>

    <div class="content-container">
      <!-- Animated header -->
      <div class="page-header">
        <h1>
          <span class="greeting">My Work</span>
          <Typewriter
              :texts="['Projects', 'Case Studies', 'Creations']"
              :speed="100"
          />
        </h1>
        <p class="subtitle">A collection of my professional and personal projects</p>
      </div>

      <!-- Interactive filter -->
      <div class="filter-controls">
        <button
            v-for="filter in filters"
            :key="filter"
            @click="activeFilter = filter"
            :class="{ active: activeFilter === filter }"
        >
          {{ filter }}
        </button>
      </div>

      <!-- Projects grid with enhanced cards -->
      <div class="projects-grid">
        <ProjectCard
            v-for="project in filteredProjects"
            :key="project.id"
            :project="project"
            @mouseenter="hoverProject = project.id"
            @mouseleave="hoverProject = null"
        />
      </div>

      <!-- Tech stack visualization -->
      <div class="tech-cloud">
        <span
            v-for="tech in techStack"
            :key="tech.name"
            :style="{
            fontSize: `${0.8 + (tech.weight * 0.3)}rem`,
            opacity: tech.weight * 0.7 + 0.3,
            transform: `rotate(${tech.rotation}deg)`
          }"
        >
          {{ tech.name }}
        </span>
      </div>
    </div>

    <!-- Floating CTA -->
    <button class="floating-cta" @click="goToContact">
      <svg viewBox="0 0 24 24"><path d="M3 3h18v2H3zm4 4h10v2H7zm4 4h6v2h-6zm-4 4h10v2H7zm4 4h6v2h-6z"/></svg>
      <span>Start a Project</span>
    </button>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ProjectCard from '../components/ProjectCard.vue'
import Typewriter from '../components/Typewriter.vue'

import { useRouter } from 'vue-router'


const filters = ref(['All', '.NET', 'Vue', 'Full Stack', 'Azure'])
const activeFilter = ref('All')
const hoverProject = ref(null)
const router = useRouter()

const projects = ref([
  {
    id: 1,
    title: 'E-Commerce Platform',
    description: 'Full-featured online store with payment integration',
    technologies: ['.NET','Vue 3', 'Node.js', 'MongoDB'],
    category: 'web',
    featured: true
  },
  {
    id: 2,
    title: 'Health Tracker App',
    description: 'Mobile application for fitness monitoring',
    technologies: ['Flutter', 'Firebase'],
    category: 'mobile'
  },
  {
    id: 3,
    title: 'Payment Gateway API',
    description: 'RESTful API for processing transactions',
    technologies: ['Node.js', 'PostgreSQL'],
    category: 'api'
  }
])

const techStack = ref([
  { name: 'C#', weight: 1, rotation: -5 },
  { name: '.NET Core', weight: 0.9, rotation: 3 },
  { name: 'Vue 3', weight: 0.9, rotation: -2 },
  { name: 'Azure', weight: 0.8, rotation: 4 },
  { name: 'SQL Server', weight: 0.7, rotation: -3 },
  { name: 'Entity Framework', weight: 0.7, rotation: 2 },
  { name: 'TypeScript', weight: 0.6, rotation: -4 },
  { name: 'Docker', weight: 0.6, rotation: 1 }
])

const filteredProjects = computed(() => {
  if (activeFilter.value === 'All') return projects.value
  return projects.value.filter(p =>
      p.category === activeFilter.value ||
      p.technologies.some(t => t.includes(activeFilter.value)))
})


const goToContact = () => {
  router.push('/contact')

  window.scrollTo(0, 0)
}
</script>

<style scoped lang="scss">
@import "../assets/styles/_shared.scss";

.projects-page {
  @extend %base-page-style;
  padding-bottom: 6rem;

  .content-container {
    position: relative;
    z-index: 2;
  }

  .page-header {
    text-align: center;
    margin-bottom: 3rem;

    h1 {
      font-size: 3.5rem;
      margin-bottom: 1rem;

      .greeting {
        display: block;
        font-size: 2rem;
        color: #42b983;
      }
    }

    .subtitle {
      font-size: 1.2rem;
      color: rgba(255, 255, 255, 0.7);
      max-width: 600px;
      margin: 0 auto;
    }
  }

  .filter-controls {
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    gap: 1rem;
    margin-bottom: 3rem;

    button {
      background: transparent;
      color: white;
      border: 1px solid rgba(255, 255, 255, 0.2);
      padding: 0.6rem 1.5rem;
      border-radius: 50px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-size: 0.9rem;

      &:hover {
        border-color: #42b983;
        color: #42b983;
      }

      &.active {
        background: #42b983;
        border-color: #42b983;
        color: white;
        box-shadow: 0 5px 15px rgba(66, 185, 131, 0.3);
      }
    }
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: 2rem;
    margin-bottom: 4rem;
  }

  .tech-cloud {
    text-align: center;
    margin-top: 4rem;
    padding: 2rem;
    background: rgba(255, 255, 255, 0.03);
    border-radius: 15px;
    border: 1px solid rgba(255, 255, 255, 0.1);
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1.5rem;

    span {
      color: #42b983;
      display: inline-block;
      transition: all 0.3s ease;
      cursor: default;

      &:hover {
        color: white;
        transform: scale(1.1) !important;
      }
    }
  }

  .floating-cta {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    background: linear-gradient(135deg, #42b983, #2c5364);
    color: white;
    border: none;
    padding: 1rem 1.5rem;
    border-radius: 50px;
    display: flex;
    align-items: center;
    gap: 0.5rem;
    cursor: pointer;
    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
    transition: all 0.3s ease;
    z-index: 10;

    &:hover {
      transform: translateY(-3px);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.3);
    }

    svg {
      width: 20px;
      height: 20px;
      fill: currentColor;
    }
  }
}

@media (max-width: 768px) {
  .projects-page {
    .page-header h1 {
      font-size: 2.5rem;
    }

    .projects-grid {
      grid-template-columns: 1fr;
    }

    .filter-controls {
      gap: 0.5rem;

      button {
        padding: 0.5rem 1rem;
        font-size: 0.8rem;
      }
    }

    .floating-cta {
      bottom: 1rem;
      right: 1rem;
      padding: 0.8rem 1.2rem;
      font-size: 0.9rem;
      -webkit-tap-highlight-color: transparent;
      &:active, &:focus {
        background: linear-gradient(135deg, #42b983, #2c5364) !important;
        outline: none !important;
      }
    }
  }
}
</style>