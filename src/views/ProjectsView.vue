<template>
  <div class="projects">
    <div class="container">
      <h1>My Projects</h1>
      <p class="subtitle">Here are some of my recent works</p>

      <div class="projects-grid">
        <ProjectCard
            v-for="project in projects"
            :key="project.id"
            :title="project.title"
            :description="project.description"
            :technologies="project.technologies"
            :image="project.image"
            :demoUrl="project.demoUrl"
            :codeUrl="project.codeUrl"
        />
      </div>
    </div>
  </div>
</template>

<script>
import ProjectCard  from "../components/ProjectCard.vue";

export default {
  name: 'ProjectsView',
  components: {
    ProjectCard
  },
  data() {
    return {
      projects: [
        {
          id: 1,
          title: 'Enterprise HR Management System',
          description: 'A comprehensive HR management solution built with ASP.NET Core and Vue.js',
          technologies: ['ASP.NET Core', 'Vue.js', 'Entity Framework', 'SQL Server'],
          image: require('@/assets/project1.jpg'),
          demoUrl: 'https://demo.example.com',
          codeUrl: 'https://github.com/yourusername/hr-system'
        },
        {
          id: 2,
          title: 'E-commerce Platform',
          description: 'Full-featured online store with payment integration',
          technologies: ['C#', '.NET 6', 'MVC', 'Stripe API'],
          image: require('@/assets/project2.jpg'),
          demoUrl: 'https://store.example.com',
          codeUrl: 'https://github.com/yourusername/ecommerce'
        },
        {
          id: 3,
          title: 'Task Management App',
          description: 'Collaborative task management application with real-time updates',
          technologies: ['SignalR', 'Blazor', 'Azure Functions'],
          image: require('@/assets/project3.jpg'),
          demoUrl: 'https://tasks.example.com',
          codeUrl: 'https://github.com/yourusername/task-manager'
        }
      ]
    }
  }
}
</script>

<style scoped lang="scss">
.projects {
  padding: 80px 0;

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
  }

  h1 {
    text-align: center;
    margin-bottom: 10px;
  }

  .subtitle {
    text-align: center;
    color: #666;
    margin-bottom: 50px;
    font-size: 1.2rem;
  }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
    gap: 30px;
  }
}
</style>