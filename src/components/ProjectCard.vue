<template>
  <div class="project-card">
    <div class="project-image">
      <img :src="image" :alt="title" />
    </div>
    <div class="project-content">
      <h3>{{ title }}</h3>
      <p>{{ description }}</p>
      <div class="tech-stack">
        <span v-for="tech in technologies" :key="tech" class="tech-badge">
          {{ tech }}
        </span>
      </div>
      <div class="project-links">
        <a v-if="demoUrl" :href="demoUrl" target="_blank" class="demo-btn">Demo</a>
        <a v-if="codeUrl" :href="codeUrl" target="_blank" class="code-btn">Code</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProjectCard',
  props: {
    title: String,
    description: String,
    technologies: Array,
    image: String,
    demoUrl: String,
    codeUrl: String
  }
}
</script>

<style scoped lang="scss">
.project-card {
  border: 1px solid #ddd;
  border-radius: 8px;
  overflow: hidden;
  transition: transform 0.3s ease;

  &:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 20px rgba(0,0,0,0.1);
  }

  .project-image {
    height: 200px;
    overflow: hidden;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  .project-content {
    padding: 20px;

    h3 {
      margin-top: 0;
    }

    .tech-stack {
      margin: 15px 0;
      display: flex;
      flex-wrap: wrap;
      gap: 8px;

      .tech-badge {
        background: #f0f0f0;
        padding: 4px 10px;
        border-radius: 20px;
        font-size: 0.8rem;
      }
    }

    .project-links {
      display: flex;
      gap: 10px;

      a {
        padding: 8px 16px;
        border-radius: 4px;
        text-decoration: none;
        font-weight: 500;

        &.demo-btn {
          background: #42b983;
          color: white;
        }

        &.code-btn {
          background: #2c3e50;
          color: white;
        }
      }
    }
  }
}
</style>