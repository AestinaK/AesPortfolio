<template>
  <div class="project-card" :class="{ featured: project.featured }">
    <div class="project-media">
      <ProjectIllustration :type="project.category || 'default'" />
      <div class="project-overlay">
        <button class="demo-btn">View Details</button>
      </div>
    </div>

    <div class="project-content">
      <h3>{{ project.title }}</h3>
      <p class="project-description">{{ project.description }}</p>

      <div class="project-tech">
        <span v-for="tech in project.technologies" :key="tech">
          {{ tech }}
        </span>
      </div>
    </div>
  </div>
</template>

<script setup>
import ProjectIllustration from './ProjectIllustration.vue'

defineProps({
  project: {
    type: Object,
    required: true
  }
})
</script>

<style scoped lang="scss">
.project-card {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 15px;
  overflow: hidden;
  border: 1px solid rgba(255, 255, 255, 0.1);
  transition: all 0.3s ease;

  &:hover {
    transform: translateY(-10px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.3);

    .project-illustration {
      transform: scale(1.05);
    }

    .project-overlay {
      opacity: 1;
    }
  }
}

.project-media {
  position: relative;
  height: 200px;
  overflow: hidden;
}

.project-overlay {
  position: absolute;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.demo-btn {
  background: #42b983;
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 50px;
  cursor: pointer;
  font-weight: 500;
}

.project-content {
  padding: 1.5rem;

  h3 {
    margin: 0 0 1rem 0;
    font-size: 1.3rem;
    color: white;
  }

  .project-description {
    color: rgba(255,255,255,0.7);
    font-size: 0.95rem;
    margin-bottom: 1.5rem;
  }
}

.project-tech {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;

  span {
    background: rgba(255,255,255,0.1);
    color: rgba(255,255,255,0.8);
    padding: 0.3rem 0.8rem;
    border-radius: 50px;
    font-size: 0.8rem;
  }
}
</style>